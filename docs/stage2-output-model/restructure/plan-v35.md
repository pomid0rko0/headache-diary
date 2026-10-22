# Restructuring plan for v35 (iteration 35, step 1 of 3)

Author of this plan: the architect of iteration 35 (Stage 2 PROCESS.md section 8, "Restructuring at iteration 35").
Object: `OUTPUT_MODEL.md` v34 (821,793 bytes; 67 elements, 117 invariants, 11 issues).
Open findings resolved by this plan: R35-01 (`reviews/review-iter-35.md`) and CA-01 to CA-19 (`audits/consistency-audit-v34.md`).
Users of this plan: the author of v35 (step 2) and the equivalence checker (step 3).

Once v35 is written, the section layout of section 2 of this plan and the ID kinds of section 4.1 are stable (PROCESS.md sections 6 and 7).

**How to read this plan.**
- "Intended change" (CHG-nn, section 12) is the only kind of change of meaning that v35 may make.
- Everything else in this plan is either a pure move (the same formal text in another place), an equivalent reformulation (checked as stated), or a prose change (prose has no formal force, section 2.1 of the model).
- **Meaning** in this plan, and for the checker: two versions have the same meaning when they admit the same MUST-conformant repertoires and the same fully conformant repertoires (model section 3.2), in every admissible context, and when every Stage 1 statement part is realised at the same level.
  - Moving a conjunct between a MUST invariant and a definitional invariant therefore changes no meaning, because both are required for MUST-conformance (model section 3.2). It is still listed (section 12, CHG-R1), so that the checker can account for it.

**Scripts.** Every check below was run by script in the architect's scratchpad (`/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/plan-v35/`, which is not in the repository and may not persist). Section 14 states each check's method, so that the checker can re-run it.

| Script | What it checks | Result |
|---|---|---|
| `parse.py`, `classify.py`, `sizes.py`, `notes_struct.txt`, `notes_paras.txt` | split v34 into items and fields; classify every invariant by the shape of its predicate; measure prose; segment long Notes | 67 E, 117 INV, 11 ISS; the families of section 1 |
| `eq_g1.py` | INV-118 with catalogue table C1 against INV-014–019, 022, 023, 025, 026, 028, 029, 108, per level, on 200,000 random small models (a free oracle for `reportedTogether`) | 0 mismatches (MUST and SHOULD) |
| `eq_g1_mut.py` | mutation test of the same: INV-018 and INV-029 put under one granularity quantifier | 1,161 mismatches (the test detects quantifier placement) |
| `eq_g2g3.py` | INV-119 with C2 against INV-013, 021, 043, 048, 065, 084, 101, 106, 107; INV-120 with C3 against INV-020, 047, 052, 090, 098, 099, 100 and the annotation conjunct of INV-092; 100,000 random models | MUST NOT: 0 mismatches. SHOULD NOT: 349 differences, all from an annotation carrying the claim about a treated-attack duration summary or a responder label (CHG-07, intended). Annotations: 0 mismatches |
| `eq_misc.py` | INV-122 nesting against the parts of INV-024, 030, 031, 033 (100,000 models); INV-064 with SD-CL (29,520 cases); INV-085 with SD-SR (1,296 cases); INV-123 role conjuncts of INV-079 under INV-001 disjointness; the E-049 `when` clause merged with the INV-070 ask (970 cases) | 0 mismatches each |
| `r3501.py` and the refined test | R35-01: the review's case 1; random single-view and two-view outputs of cycle lines | see section 10, R35-01: the refined conjunct leaves wrong window marks only on lines that have not ended |

---

## 0. Summary

- **Families found.** 38 v34 invariants are wholly instances of generic rules: 36 go into 7 of the 8 new generic invariants (INV-118 to INV-123 and INV-125; per invariant 13, 9, 7, 1, 1, 3 and 2), and 2 (INV-007, INV-054) go into the placement-marker rule W2. 25 more lose individual conjuncts to those rules or to a new placement marker. In v35 the generic rules are 8 new invariants (INV-118 to INV-125) plus one notation rule (W2, placement markers on reference attributes). The 38 absorbed invariants are withdrawn as merged (section 11). v35 has 87 invariants (117 − 38 + 8) and the same 67 elements. No element is withdrawn.
- **Layout.** Sections 1 to 10 and 12 keep their numbers and roles.
  - Section 4 becomes "Model overview and output catalogue", with 45 catalogue rows (OC-01 to OC-45) and three formal column tables (C1 per-period availability, C2 prohibited claims, C3 required labels and caveats).
  - Section 11 (the search log, which moves to `RATIONALE.md`) becomes "Source data tables" (SD-…): values that sources fix, written once, in case tables with formal force.
  - The notation gains two defined constructs: **case tables** (section 2.11) and **placement markers** (rule W2, section 2.5). Conformance gains **level-indexed invariants** (section 3.3, item 7), the enumeration `Level`, and the general rule on **facts the context does not state** (R-MCF, section 3.8).
- **Intended changes of meaning:** 7 (CHG-01 to CHG-07), plus 1 reclassification without change of admitted outputs (CHG-R1). See section 12.
- **Size.** `OUTPUT_MODEL.md` goes from 822 KB to about 400–450 KB, and the new `RATIONALE.md` is about 300–350 KB (section 14.3).
- **Decisions for the human:** section 15.

---

## 1. Diagnosis

### 1.1 Method

Every invariant's `omn` block was classified by the shape of its predicate (`classify.py`): availability over `Rep` with `reportedPerPeriod`/`reportedTogether`; a prohibition `¬ ∃ … claims`; `annotated(`; a placement `∈ viewOf(…).content` or `∈ v.content`; a tie to `ctx.subject`, `eventOn`, `startOf` or the available results; and `≤ … lengthDays` or `daysOf` bounds. Each candidate family was then read predicate by predicate. A family is kept as one rule only where the predicates have the same form up to parameters that a table can carry. Equivalence was checked by script where the form allows it (section 0).

### 1.2 Families that are instances of one rule

| # | Family (the rule stated once) | v34 items, whole | v34 items, conjuncts only | Evidence from the formal blocks | v35 |
|---|---|---|---|---|---|
| F1 | **Per-period availability:** a per-period measure is available, for every period of the selected time range, at some granularity of a stated kind, for the contexts that meet a condition, in the stated type scopes, together in one view where Stage 1 asks for them together | INV-014, 015, 016, 017, 018, 019, 022, 023, 025, 026, 028, 029, 108 (13) | — | All 13 have the form `∃ g ∈ G • ∀ c ∈ Ctx • c.granularity = g ∧ A(c) ⇒ ⋀ reportedTogether(c, Ks, sc)`. INV-014/016/017 differ only in the measure. INV-108 is two such formulas, one per measure, each with its own `∃ g`. INV-025 equals the form with `G = {calendarWeek}` (section 5, INV-118) | INV-118 + C1 (14 clauses) |
| F2 | **Prohibited claims:** an element of a stated kind is not presented with a stated claim, either by itself or by a label or caveat that qualifies it | INV-013, 021, 043, 048, 065, 084, 101, 106, 107 (9) | — | All 9 have the form `¬ ∃ x ∈ B • C ∈ x.claims` (INV-048 and INV-084 also test the qualifying annotations; INV-021 and INV-065 do not, a difference with no Stage 1 basis, CHG-07). INV-043 and INV-084 are implied by INV-101 at the same level and are kept as catalogue cells for traceability | INV-119 + C2 (9 cells) |
| F3 | **Required labels and caveats:** an element of a stated kind carries an annotation of a stated kind | INV-020, 047, 052, 090, 098, 099, 100 (7) | INV-092 (`annotated(x, exploratoryMeasure)`) | All have the form `∀ x ∈ B • annotated(x, k)` | INV-120 + C3 (12 cells) |
| F4 | **Placement of referenced content:** an item that a holder refers to as its content is shown in the holder's view | INV-007, INV-054 (2) | INV-035, 041, 050, 059, 062, 072, 078, 087, 092, 109 | `y ∈ viewOf(x).content` or `y ∈ v.content` for a reference attribute of x or v. INV-003 Notes list this class and the "missing case" CA-09 belongs to it | Rule W2: markers on 19 reference attributes (section 5, W2) |
| F5 | **Values within their period:** a number of days (or a time) within a period does not exceed the period's length | INV-005 (1) | INV-012 (covered days), INV-032 (days of a level), INV-033 (pain time, days with a symptom, caregiver days) | `n ≤ … .lengthDays` or `≤ daysLong(… .lengthDays)` | INV-121 |
| F6 | **Nested counts:** in one view, for periods with the same dates and the same type scope, a count of days with a narrower property does not exceed the count with the wider one | INV-030 (1) | INV-024 (4 bounds), INV-031 (2 bounds), INV-033 (functional-impact bounds) | `∀ a ∈ daysOf(v, k₁, p, sc); b ∈ daysOf(v, k₂, p, sc) • a ≤ b` for pairs (k₁, k₂) | INV-122 with the nesting relation `nestedIn` (E-014) |
| F7 | **Shown context facts:** a value that names a fact of the context (a treatment course, a course event, a start of withdrawal, an acute medication, an available result) names a fact that the context states. This is the "truth of a shown fact" class of the oscillation checks (R30-01, R31-01, R32b-02) | INV-036, INV-113, INV-117 (3) | INV-056, 067, 068, 075, 079, 082, 085, 112 | membership tests of `ctx.subject.*`, `eventOn`, `startOf`, `stopped`, available administrations, on attributes of 13 element kinds (fix 32's attribute table) | INV-123 with `ShownFact`, `stated` (E-008) and `factsShown` (E-001) |
| F8 | **Labels whose definition Stage 1 fixes** | INV-009, INV-010 (2) | — | `∀ l : DefinitionLabel • l.measure = m ⇒ l.definition = d` for two (m, d) at MUST and SHOULD | INV-125 + case table SD-DF |
| F9 | **Dated phases of one output describe one history** (the class of R35-01) | — (new) | INV-089 (bout–remission non-overlap within one cluster view) | Non-overlap holds only inside the sequence of one view (INV-087 for the menstrual-relation view, INV-089 for the cluster view). Nothing holds across views or for lines of other views | INV-124 (R35-01, CHG-01, CHG-02) |

Families F1, F2, F3 and F8 have levels that differ per case. They become **level-indexed invariants** (section 3.3, item 7, new): one predicate Φ(l) whose instance for level l holds at that level, reading its cases from a catalogue or source-data table whose rows carry the level.

### 1.3 Considered and kept specific (with reason)

| Items | Why not merged |
|---|---|
| INV-003, INV-008, INV-011, INV-097 | Already generic over all views or all comparisons. |
| INV-034, 037, 039, 040, 044, 049, 055, 071, 077, 081, 083, 086, 088, 094, 095, 096, 102, 103 (availability of views and items) | Each states a different occasion (each treatment, event, withdrawal, selection, result) and content that is entangled with the same witness view (`∃ v • A(v) ∧ B(v)`, for example INV-088). A generic form would only rename the per-case content. Their level and applicability appear in the catalogue's index columns. |
| INV-027, INV-039, INV-069, INV-105 (comparability: `onSameScale`, `inSameForm`, one domain) | The anchored form was chosen by fix 32 over an all-pairs form, and the places were selected by Stage 1 wording (oscillation check 32, watch point 3). A generic "all compared values comparable" rule would be the all-pairs form, which fix 32 declined. |
| INV-114, INV-115, INV-059 (`tp.treatment = rc.treatment`), INV-079 (`r.treatment`, `a.treatment`, `s.drug`), INV-061, INV-038, INV-074 | Identity ties between an item and the items it refers to. They are not context facts (F7). A generic "same treatment for every referenced item" rule over `refs` would also forbid, among a responder label's other values, an item of another treatment, which OUT-020's open list ("for example") permits. |
| INV-045, 046, 053, 058, 061, 063, 064, 074, 082, 087, 089, 116 (value relations) | Formulas that a source or a definition fixes for one element (PROCESS section 6a: "specific to that output"). INV-064's thresholds move to table SD-CL, and INV-082's value sets to SD-IN and SD-GB, but the relations stay. |
| INV-091, INV-093 | OUT-037-specific (a role and a companion value). |
| INV-042, INV-060, INV-066, INV-083 (specific companions) | Each is a companion that one Stage 1 requirement names, with its own relation (residual burden of a change, adherence over an evaluation window, headache days next to a screening result, codes of the three-month view). |

---

## 2. New layout

### 2.1 `OUTPUT_MODEL.md` (v35)

```
# Headache diary — formal model of output data (Stage 2)
Version: v35 · Iteration: 35 · Status: under review
Baseline: Stage 1 OUTPUT_REQUIREMENTS.md v18 (converged)
Companion: RATIONALE.md v35

## 1. Scope and exclusions                 v34 text, unchanged
## 2. Notation                             2.1–2.10 as v34 with the edits of plan section 3; 2.11 Case tables (new)
## 3. Conformance                          3.1–3.7 as v34 with the edits of plan section 3; 3.8 Facts the context does not state (new, R-MCF)
## 4. Model overview and output catalogue
### 4.1 Layers                             v34 section 4, shortened; CA-19 corrected
### 4.2 Catalogue: row IDs and columns
### 4.3 The catalogue                      one row per kind of output, OC-01 … OC-45 (index columns)
### 4.4 Formal columns of the catalogue    `enum CatalogueRow`; case tables C1, C2, C3
## 5. Model elements                       5.1–5.10 as v34, E-001 … E-067, same order and IDs
## 6. Invariants
### 6.0 Generic invariants                 INV-118 … INV-125 (new)
### 6.1–6.12                               as v34, the kept invariants in v34 order
## 7. Traceability                         one row per OUT; new column template (plan section 9.3)
## 8. Stage 1 issues for the human         ISS-01 … ISS-12 (ISS-07 withdrawn) + ISS-13 (new, CA-01)
## 9. Withdrawn and merged items           v34 table + the 38 merged invariants
## 10. Sources                             v34 table, unchanged
## 11. Source data tables                  SD-IC, SD-DF, SD-CLS, SD-CMB, SD-FX, SD-ER, SD-RC, SD-CL, SD-IN, SD-GB, SD-SC, SD-SR, SD-ET
## 12. Change log                          one short entry per version (plan section 9.3)
```

Item layout is unchanged (PROCESS.md section 6): elements have Definition, Meaning, Conformance, Realises, Evidence, Notes; invariants have Predicate, Reading, Conformance, Realises, Evidence, Notes. A merged invariant's heading and fields are removed from section 6 and listed in section 9.

### 2.2 `RATIONALE.md` (v35)

```
# Headache diary — rationale of the output model (Stage 2)
Version: v35 (companion of OUTPUT_MODEL.md v35)

## 1. Purpose and rules
   The model governs; a difference between the two is a defect of RATIONALE.md (PROCESS.md section 6a).
   Entry IDs, entry kinds, entry layout (below). No entry states a constraint that the model does not state.
## 2. Entries, in model order
### 2.1 Notation and conformance           anchors SEC-2.n, SEC-3.n
### 2.2 Catalogue rows                      anchors OC-NN, C1-NN, C2-NN, C3-NN
### 2.3 Elements                            anchors E-001 … E-067
### 2.4 Invariants                          anchors INV-…
### 2.5 Traceability                        anchors OUT-NNN (only where a reading of a Stage 1 statement is argued)
### 2.6 Stage 1 issues                      anchors ISS-NN
### 2.7 Source data rows                    anchors SD-XX-NN
### 2.8 Withdrawn (merged) invariants       anchor = the v35 item they went into; v34 ID named in the entry
## 3. Search log                            SL-001 …: v34 section 11, verbatim, one entry per paragraph or table
```

**Entry ID:** `<anchor>/<kind><nn>`, for example `E-041/Q07`, `INV-055/S01`, `SD-ER-03/Q01`, `OC-23/D01`, `ISS-12/Q02`, `SEC-3.8/D01`.
- The anchor is the ID of the model item the entry concerns.
- `nn` is two digits, numbered per anchor and kind, in v34 order of appearance.
- IDs are stable under PROCESS.md section 7: never renumbered or reused. An entry that becomes wrong is corrected in place, or marked "withdrawn in vNN" and kept.

**Entry kinds:**

| Kind | Content | Default source in v34 |
|---|---|---|
| `Q` | Evidence quote: source ID, URL (from model section 10 or Stage 1 section 5), location, verbatim quote, translation where the source is not in English, and the parenthetical notes on the text layer, all verbatim | Evidence fields; quotes inside Notes |
| `D` | Design reason or reading of a source or of Stage 1 | Notes paragraphs that argue why |
| `X` | Rejected alternative | fix-log reasons cited in Notes ("option (b) was not taken …") |
| `N` | What is deliberately not modelled | "not modelled", "out of scope", "is not part of the output", "Named, but not evaluation time points" |
| `S` | Satisfiability argument | sentences or paragraphs beginning "Satisfiab…" |
| `W` | Worked example with dates | "For example, for a treatment started on …" |

**Entry layout** (one heading per entry):

```
### E-041/Q07
- Kind: Q
- Concerns: E-041; SD-ER-05
- Source: [S-018] — URL
- Location: <the v34 location parenthetical, verbatim>
- Quote: "<verbatim>"
- Translation: "<verbatim from v34>"            (only where v34 has one)
```

For kinds D, X, N, S and W, the entry has `Kind`, `Concerns` and `Text` (moved verbatim from v34, with the reference updates of plan section 9.1, rule P0). Model Evidence fields become: `Stage 1 OUT-NNN[, OUT-…]; [S-1NN] E-041/Q07, [S-018] E-041/Q05 …` (source ID and entry ID only).

---

## 3. Notation and conformance changes (exact)

All edits are minimal and are defined here. The author inserts them as stated.

### 3.1 Section 2.11 Case tables (new)

Text to insert (normative):

> **2.11 Case tables.** A case table is a table of the model that states axioms or definitions by cases, one row per case. It is a way of writing OMN paragraphs and describes no storage. Its caption, the line directly above it, reads `Case table <ID> — <form>` and names the OMN declarations it gives cases for.
>
> - **Formal and informative columns.** A column whose header is code-formatted (`` `…` ``) is formal. Every other column (for example Row, Source, Rationale) is informative and has no formal force.
> - **Cells.** A formal cell holds one OMN term or formula in code format. In a cell, `\|` stands for `|`, and `<br>` is white space. The cell `—` states no case.
> - **Form V: constants of a value type.** The caption names a value type T, and may name a collecting constant S. The key column, headed `` `k` ``, lists new constant names, and every other formal header is a component name of T; every component of T has a column. The row with key k and cells e₁ … eₙ denotes `const k : T` and `axiom k = T(a₁ ↦ e₁, …, aₙ ↦ eₙ)`. If the caption names S, the table also denotes `const S : set1 T ≙ {k₁, …, kₘ}`, the set of its keys.
> - **Form M: members of a set.** The caption names `const S : set1 T`. Every formal header is a component name of T, and each row denotes the member T(a₁ ↦ e₁, …). The table denotes `const S : set1 T ≙ {the rows' members}`.
> - **Form C: cases of functions and predicates.** One or more key columns are headed `` `x₁ : K₁` ``, …. Each key cell is a ground term of its type. Every other formal header is an application `f(x₁, …, p₁, …)` of a function or predicate declared in an `omn` block, with the key variables first and further parameters p declared there.
>   - If f is a **given** function (section 2.3), each non-`—` cell e denotes the axiom `f(keys) = e`, or, for a 𝔹-valued f, `f(keys)` for the cell `true` and `¬ f(keys)` for `false`.
>   - A given **partial** function (`⇸`) whose cases are given by a case table has as its domain exactly the keys whose cell is not `—`.
>   - If f is declared `fun f(x₁ : K₁, …, p : P) : T ≙ table N default e` or `pred f(…) ≙ table N`, the table is f's definition by cases: f(x…, p…) is the cell of the row whose keys are x…, and the default (for a predicate, false) where no row has these keys or the cell is `—`.
> - **Paragraph forms.** `axiom table N` states the axioms of case table N. `const S : set1 T ≙ table N`, `fun f(…) : T ≙ table N default e` and `pred p(…) ≙ table N` refer to a case table as the definition.
> - **Type checking.** The keys of a table are pairwise distinct. Every cell is well typed (section 2.10) with the key variables and parameters in scope.

Edits to section 2.3: add the three phrases `axiom table N`, `≙ table N [default e]`, and the sentence "Case tables (section 2.11) give cases of given and defined functions and constants".

### 3.2 Rule W2: placement markers (section 2.5, new paragraph after rule W1)

> **Rule W2 (placement).** An attribute whose type mentions `→R` may carry a placement marker after its level and `when` clause: `shown` (definitional), `shown MUST` or `shown SHOULD`, optionally followed by its own `when ψ` (with `self` and `ctx` as in section 2.5).
>
> For every atom x of the type for which ψ holds, every atom y that x.a references satisfies `∀ h ∈ home(x) • y = h ∨ y ∈ h.content`, where:
>
> `fun home(x : Element) : set View ≙ {v ∈ {x} ∩ View • v} ∪ {i ∈ {x} ∩ Item • viewOf(i)}`
>
> (the view itself for a view, and the item's view for an item). A marker without a level is part of the element's definition (section 3.3, item 5). A marker with a level holds at that level (section 3.3, item 8).

Syntax of an attribute declaration (section 2.5) becomes `a : T [derived] level [when φ] [shown [MUST | SHOULD] [when ψ]]`. Typing rule: a marker only on an attribute whose type mentions `→R`.

Replace in section 2.5 "for the other references, the invariant of the element that holds them" by "for the other references, a placement marker (rule W2)".

### 3.3 Conformance additions (section 3)

- **Section 3.1** gains: `enum Level ::= must | should | may | shouldNot | mustNot` (an `omn` block; the levels as values, used by the catalogue and source data tables).
- **Section 3.3, item 4**, add: "except a level-indexed invariant (item 7), which has one level per instance."
- **Section 3.3, item 7 (new): level-indexed invariants.**
  > An invariant whose Conformance field reads "level-indexed" has a predicate Φ with one free variable l of type `Level`. For each l ∈ {must, should, shouldNot, mustNot}, the instance Φ[l] is a constraint at level MUST, SHOULD, SHOULD NOT or MUST NOT. The instance Φ[may] imposes nothing.
  >
  > An instance at SHOULD NOT or MUST NOT has the form ¬ F (item 4). The level of every case that an instance reads from a table follows the Stage 1 strength of the statement part named in that row (item 6).
- **Section 3.3, item 8 (new): placement markers.** "A placement marker `shown L` (rule W2) holds at level L for every atom of the type for which its `when` clause holds. `shown` without a level is definitional (item 5)."
- **Section 3.3, item 1**, add: "For per-period measures, the repertoire invariant is INV-118 with its catalogue clauses (table C1)".
- **Section 3.2 (CA-11).** Replace the three comments of the `omn` block that carry semantic conditions by sentences after the block:
  > `Ctx` is the set of `OutputContext` values that satisfy the context invariants (INV-001). `Rep ⊆ Ctx × Output`. For every output o, (ctx(o), o) ∈ Rep, and no output is paired with two contexts. `parts(o)` = {o} ∪ o.views ∪ {i | v ∈ o.views ∧ i ∈ v.content}.
  
  These sentences are normative (section 3 is conformance semantics). The comments are reduced to their glosses.
- **Section 3.4.** Replace references to INV-014 to INV-017, INV-108, INV-028, INV-037 and INV-057 by "INV-118 (C1-01 to C1-06, C1-13), INV-037 and INV-057". The argument on the reading of OUT-001's "Frequency outputs" moves to `SEC-3.4/D01` (verbatim), and section 3.4 keeps one sentence: "OUT-001's frequency outputs are read as the frequency measures of OUT-004 to OUT-007 (OUT-009 wording); see ISS-04."
- **Section 3.8 (new): facts the context does not state.** Text in plan section 7.

### 3.4 Other notation edits (CA-11, CA-17, CA-18)

- **Section 2.3 (CA-11).** "`⇸` instead of `→` declares a given partial function whose domain is stated in its comment" becomes:
  > … whose domain is stated by a case table (section 2.11), by an axiom, or, for the library functions of section 2.8, in that section's list, which defines the library. Where none of these states it, the model constrains the domain only through the invariants that use `dom` (for `classOf`, INV-001).
  
  The domain comments of `publishedRecall`, `scoreRange` and `classOf` are deleted (the first two are fixed by SD-IN).
- **Section 2.2.** "Comments … have no formal force" stays unchanged; after the edits above, no comment carries a normative condition.
- **Section 2.4 (CA-17).** "(used only for parameters of predicates and for the semantic constants of section 3.2)" becomes "(used for parameters of predicates and functions, for the result types of defined functions and the components of values that hold sets of atoms, for example `fiDays` (E-030) and the catalogue columns (section 4.4), and for the semantic constants of section 3.2)".
- **Section 2.8 (CA-18).** "under the week convention of the output" becomes "under the week convention of the diary (one convention for all its outputs)".
- **Section 2.9.** Add: "In an output-scope invariant, a quantifier `∀ x : Element` ranges over the atoms of o, so that a table cell that names an element type (for example `View` in table C3) is used only through such a quantifier."

---

## 4. Output catalogue

### 4.1 New ID kinds (stable under PROCESS.md section 7)

| ID kind | Form | Meaning | OMN name |
|---|---|---|---|
| Catalogue row | `OC-NN` (two digits; `OC-100` and up if ever needed, never renumbered) | one kind of output that a reader is shown | the constant `ocNN` of `enum CatalogueRow` (`OC-07` ↔ `oc07`) |
| Formal column case | `C1-NN`, `C2-NN`, `C3-NN` | one row of a case table of the catalogue's formal columns (section 4.4) | — (rows of case tables) |
| Source data row | `SD-<table>-NN`, tables `IC`, `DF`, `CLS`, `CMB`, `FX`, `ER`, `RC`, `CL`, `IN`, `GB`, `SC`, `SR`, `ET` | one row of a source data table (section 6) | — |
| Rationale entry | `<anchor>/<kind><nn>` | one entry of `RATIONALE.md` (section 2.2) | — |
| Search-log entry | `SL-NNN` | one entry of the search log in `RATIONALE.md` | — |
| Change | `CHG-NN`, `CHG-R1` | intended changes of v35 (section 12); used in this plan and in `fixes/fix-iter-35.md` | — |

A withdrawn row, case or entry keeps its ID and is listed as withdrawn (model section 9 for OC, C and SD rows; in place for rationale entries).

### 4.2 Columns of the catalogue (model section 4.3)

The catalogue table is an **index**. Its cells name items by ID, state levels, and quote Stage 1 wording (Audience lines, applicability phrases). It does not restate a predicate. The formal force of the catalogue lies in the enumeration `CatalogueRow` and in the case tables C1, C2 and C3 (section 4.4), which generic invariants quantify over.

| Column | Content | Formal? |
|---|---|---|
| Row | `OC-NN` | the enumeration constant |
| Output kind | name, as Stage 1 names it, and the element IDs | index |
| Audience | the Stage 1 Audience line(s) of the OUTs realised, verbatim (moved here from the Meanings, which no longer state audiences) | index |
| Period and granularity | e.g. "per reporting period; calendar month or 28-day period" | index (formal in C1 or in the named invariant) |
| Applicability | the Stage 1 condition phrase and the OMN predicate that states it (e.g. "patients with migraine — `hasType(c, c1)`"), or "R-MCF (n)" | index |
| Availability | level and the item that states it (`INV-NNN`, `C1-NN`), and the definitional invariants of the kind | index |
| Shown with it | companions, by ID: periods (INV-003), labels (INV-008), completeness (INV-011), W2 markers, C3 cells, specific companions (INV-060, INV-066, …), context facts (INV-123) | index |
| Prohibited | C2 cells, and INV-091 | index |
| Realises | OUT IDs (the union of the Realises fields of the items of the row) | index, checked by script against Realises fields |

The plan's table below has one more column, **Absorbs (v34)**, which is for `fixes/fix-iter-35.md` and the checker. The model's table omits it.

### 4.3 The 45 rows

Abbreviations: "label" = INV-008, "completeness" = INV-011, "def." = definitional.

| Row | Output kind (elements) | Audience (Stage 1) | Period and granularity | Applicability | Availability | Shown with it | Prohibited | Realises | Absorbs (v34) |
|---|---|---|---|---|---|---|---|---|---|
| OC-01 | Summary output and its reporting period (E-002, E-003, E-004 `Item`, E-005) | OUT-001: patients, primary-care clinicians, specialists, researchers; OUT-038: patients, clinicians | the period each view covers | every output | structural; covered period MUST (E-003, INV-003); def. INV-002 | its periods (INV-003); caveats C3-01; completeness | C2-01 | OUT-001, OUT-034, OUT-035, OUT-038 | E-002, E-003, E-005, INV-002, INV-003, INV-099, INV-101 |
| OC-02 | Time series of consecutive periods (E-006) | as the views that show it | calendar months, 28-day periods, calendar weeks | — | structural; def. INV-004 | its periods (INV-003) | — | OUT-001, OUT-004, OUT-009, OUT-015, OUT-028 | E-006, INV-004 |
| OC-03 | Definition label (E-011) | OUT-002: clinicians, researchers | per view | views that report the measure (`reports`) | SHOULD (INV-008); def. INV-111; fixed definitions (INV-125: SD-DF-01 MUST, SD-DF-02 SHOULD) | — | — | OUT-002, OUT-004, OUT-005, OUT-006, OUT-007, OUT-028 | E-011, INV-008, INV-009, INV-010, INV-111 |
| OC-04 | Completeness indicator (E-013) | OUT-003: clinicians, researchers, patients | each reporting period of a summary measure | — | SHOULD (INV-011); def. INV-012, INV-121 | — | C2-02 | OUT-003, OUT-034 | E-013, INV-011, INV-012, INV-013 |
| OC-05 | Headache days (E-015; E-014) | OUT-004: patients, primary-care clinicians, specialists, researchers | per period; calendar month or 28-day period | every subject | MUST (C1-01); def. INV-006, INV-121, INV-122 | label (fixed: SD-DF-01); completeness | — | OUT-001, OUT-002, OUT-004 | E-014, E-015, INV-005, INV-006, INV-014 |
| OC-06 | Migraine days (E-016) | OUT-005: patients, clinicians, researchers | calendar month or 28-day period | "For patients with migraine" — `hasType(c, c1)` | MUST (C1-02) | label; completeness | — | OUT-001, OUT-002, OUT-005 | E-016, INV-015 |
| OC-07 | Moderate/severe headache days (E-017) | OUT-006: clinicians, researchers, patients | calendar month or 28-day period | every subject; MUST "where provided" — `provides(…)` | SHOULD (C1-03); MUST where provided (C1-04) | label; completeness | — | OUT-001, OUT-002, OUT-006 | E-017, INV-016, INV-108 (first measure) |
| OC-08 | Number of attacks (E-019 `AttackCount`) | OUT-007: clinicians, researchers | calendar month or 28-day period | every subject; MUST where provided | SHOULD (C1-05); MUST where provided (C1-06) | label (fixed: SD-DF-02); completeness | — | OUT-001, OUT-002, OUT-007, OUT-013 | E-019, INV-017, INV-108 (second measure) |
| OC-09 | Headache-free days, symptom-free days, periods without migraine days (E-020, E-021, E-022) | OUT-008: patients, clinicians, researchers | per reporting period | every subject (ISS-03) | MAY; SHOULD in the clinician-facing summary (INV-104; ISS-04); def. INV-031, INV-122 | exploratory label MAY (C3-02); label where a mark is shown; completeness | — | OUT-008 | E-020, E-021, E-022 |
| OC-10 | Time-course view with treatment markers (E-034, E-035) | OUT-009: patients, clinicians, researchers | series of calendar months or 28-day periods; calendar weeks where weekly granularity is clinically relevant | every subject; weekly: `ctx.weeklyGranularityRelevant` | SHOULD (INV-034); content SHOULD (INV-035) | series and markers (W2 SHOULD, E-035); marker facts (INV-123) | — | OUT-009, OUT-034, OUT-035 | E-034, E-035, INV-034, INV-035, INV-036 |
| OC-11 | Intensity summary (E-023) | OUT-010: clinicians, patients | per reporting period | every subject | SHOULD (C1-07); between periods (INV-039, OC-33); def. INV-032, INV-121 | scale SHOULD (E-023); label where a distribution is shown | — | OUT-010, OUT-021, OUT-029, OUT-035 | E-023, INV-018, INV-032 |
| OC-12 | Duration summary (E-024) | OUT-011: clinicians, patients | per reporting period | every subject | SHOULD (C1-08); def. INV-121 | "influenced by acute treatment" (C3-03) | C2-03 | OUT-011, OUT-013 | E-024, INV-019, INV-020, INV-021 |
| OC-13 | Associated symptoms and most bothersome symptom across periods (E-025, E-026) | OUT-012: clinicians, researchers, patients | per reporting period | "For migraine" — `hasType(c, c1)` | SHOULD (C1-09); def. INV-033, INV-121 | — | — | OUT-012, OUT-021 | E-025, E-026, INV-022 |
| OC-14 | Aura count and duration (E-027) | OUT-013: clinicians, patients | per reporting period | "patients with migraine with aura" — `hasType(c, c1_2)` | MAY (no invariant) | — | — | OUT-013 | E-027 |
| OC-15 | Acute-medication days: total, per ICHD-3 8.2 class, per drug (E-028, E-029) | OUT-014: clinicians, patients, researchers | per reporting period | every subject; every acute medication used up to the as-of date (E-008) | MUST (C1-10); def. INV-024, INV-122; usage fact (INV-123) | completeness | — | OUT-014, OUT-015, OUT-016, OUT-029 | E-028, E-029, INV-023, INV-024 |
| OC-16 | Weekly acute-medication view (E-036) | OUT-015: clinicians, patients | calendar weeks | every subject | SHOULD (C1-11) | completeness | — | OUT-015 | E-036, INV-025 |
| OC-17 | Medication-overuse indicator (E-032) | OUT-016: clinicians (primary), patients (in plain language) | calendar month or 28-day period, with its span | each class of the subject's acute medications; combined use | MUST (INV-044); def. INV-045, INV-046 | review prompt (C3-04 MUST); clinical-interpretation caveat (C3-05 SHOULD) | C2-04 | OUT-014, OUT-016, OUT-038 | E-032, INV-044, INV-045, INV-046, INV-047, INV-048, INV-100 (indicator) |
| OC-18 | Withdrawal follow-up view (E-039) | OUT-017: clinicians, patients | from the start of withdrawal; series of whole periods from it; NICE review window | "For patients withdrawing from overused medication": each start of withdrawal in `ctx.subject.withdrawalStart` | SHOULD (INV-049); content SHOULD (INV-050); def. INV-051 | series (W2 SHOULD); worsening label (C3-06); start fact (INV-123) | — | OUT-017 | E-039, INV-049, INV-050, INV-051, INV-052, INV-113 |
| OC-19 | Change from a reference period (E-040) | OUT-018: clinicians, patients, researchers; OUT-019: clinicians, patients | the two compared periods | wherever shown | def. INV-053; in a response comparison both forms MUST (E-040 `when`) | the two values, in a response comparison (W2 MUST); periods (INV-003); residual burden (INV-060); label; completeness | — | OUT-018, OUT-019, OUT-020, OUT-036 | E-040, INV-053, INV-054 |
| OC-20 | Evaluation time point (E-041, E-042; SD-ER) | OUT-018: clinicians, patients, researchers | anchor date; date or window of evaluation | rules applicable to the treatment (`applicable`, E-041) | MUST with each response comparison (INV-059); def. INV-058 | — | — | OUT-018, OUT-036 | E-041, E-042, INV-058 |
| OC-21 | Response comparison (E-043) | OUT-018: clinicians, patients, researchers | baseline month; monthly on-treatment periods | "For each preventive treatment", whose start the context states — R-MCF (1) | MUST (INV-055); content MUST (INV-056, INV-057, INV-059) | values and changes (INV-003, INV-056, W2); time points (W2 MUST); adherence (INV-066); acute summaries per phase (INV-071); functional impact (INV-027); start fact (INV-123) | C2-05 | OUT-001, OUT-018, OUT-036 | E-043, INV-055, INV-056, INV-057, INV-059, INV-106 |
| OC-22 | Residual burden (E-044) | OUT-019: clinicians, patients | a calendar month or 28-day period within the compared period | "Wherever the output shows a relative (percentage) change in migraine or headache days" (compared period of at least 28 days, CHG-03, ISS-13) | SHOULD (INV-060); def. INV-061 | — | — | OUT-019 | E-044, INV-060, INV-061 |
| OC-23 | Responder label and its named criterion (E-045, E-046; SD-RC, SD-CL) | OUT-020: clinicians, patients | evaluated on-treatment periods | "If the output displays a responder or non-responder label" (MAY) | MAY; content SHOULD (INV-062); def. INV-063, INV-064, INV-114, INV-116 | comparison, residual burden, other values (W2 SHOULD); clinical-interpretation caveat (C3-07); treatment fact (INV-123) | C2-06 | OUT-020, OUT-025, OUT-038 | E-045, E-046, INV-062, INV-063, INV-064, INV-065, INV-100 (label), INV-114, INV-116, INV-117 |
| OC-24 | Days with migraine or moderate-to-severe headache, the count of the IHS position statement 2025 (E-018) | OUT-020: clinicians, patients | each evaluated month of a control-level label | with control-level labels | SHOULD with such a label (INV-062); def. INV-031 (relation to migraine days under `ihs2025MigraineDay`) | — | — | OUT-020 | E-018 |
| OC-25 | Adherence summary (E-047) | OUT-039: clinicians, patients | an evaluation window of the response comparison | "For each preventive treatment" | SHOULD next to the comparison (INV-066), in the treatment history (INV-109), in the clinician-facing summary (INV-104); def. INV-067 | completeness of its window; treatment fact (INV-123) | — | OUT-039 | E-047, INV-066, INV-067 |
| OC-26 | Treatment review view (E-048) | OUT-021: clinicians, patients | the same baseline and on-treatment periods | each preventive treatment whose start the context states — R-MCF (1) | MUST (INV-102); content MUST (INV-068), SHOULD where provided (INV-069) | treatment fact (INV-123) | — | OUT-021, OUT-023, OUT-036 | E-048, INV-068, INV-069, INV-102 |
| OC-27 | Post-stop monitoring view (E-049) | OUT-022: clinicians, patients | from the first changed day; on-treatment period; original baseline | each stop, pause or dose reduction of a preventive treatment, whether or not its start is stated — R-MCF (2) | SHOULD (INV-103); content SHOULD (INV-070, E-049 `when` clauses); def. INV-112 | event fact (INV-123) | — | OUT-022, OUT-036 | E-049, INV-070, INV-103, INV-112 |
| OC-28 | Acute-treatment summary, outcome summaries, treated-attack lines (E-050, E-051, E-052, E-053; SD-ET) | OUT-023: clinicians, patients | the selected time range; baseline and on-treatment periods; periods named by other rows | "For each acute medication" used up to the as-of date | SHOULD (INV-071); content SHOULD (INV-072, INV-073, INV-076); def. INV-074, INV-075 | outcome summaries and lines (W2 SHOULD); medication fact of lines (INV-123) | C2-07 | OUT-012, OUT-021, OUT-023, OUT-024, OUT-031 | E-050, E-051, E-052, E-053, INV-071, INV-072, INV-073, INV-074, INV-075, INV-076, INV-107 |
| OC-29 | Treatment history: view, class groups, treatment lines (E-054, E-055) | OUT-024: clinicians (primary), patients | the dates of each course | every treatment of the subject | SHOULD (INV-077); content SHOULD (INV-078, INV-109); def. INV-079 | groups (W2 SHOULD) and their lines (INV-078); response summaries and adherence (W2 SHOULD); course facts (INV-123) | — | OUT-024, OUT-034, OUT-039 | E-054, E-055, INV-077, INV-078, INV-079, INV-109 |
| OC-30 | Scheme-window view (E-056) | OUT-025: clinicians preparing reimbursement or registry documentation | the selected windows | contexts with a scheme selection — R-MCF (3) | MAY; def. INV-080 | — | — | OUT-025 | E-056, INV-080 |
| OC-31 | Instrument result (E-057, E-058; SD-IN, SD-GB) | OUT-026: clinicians, patients, researchers | completion date | "Where results of validated instruments are available" — R-MCF (4) | SHOULD (INV-081); def. INV-082 | clinical-interpretation caveat where a category is shown (C3-08); availability fact (INV-123) | — | OUT-020, OUT-021, OUT-025, OUT-026, OUT-034, OUT-036, OUT-038 | E-057, E-058, INV-081, INV-082, INV-100 (result) |
| OC-32 | Functional impact days (E-030) | OUT-027: clinicians, patients, researchers | per reporting period | every subject | SHOULD (C1-12); comparison with the baseline period SHOULD (INV-027); def. INV-121, INV-122 | — | — | OUT-027, OUT-036 | E-030, INV-026, INV-027 |
| OC-33 | Comparison of selected periods (E-037) | OUT-001: patients, primary-care clinicians, specialists, researchers; OUT-010, OUT-027 | the selected periods | two or more selected periods — R-MCF (3) | MUST for equal lengths (INV-037); intensity SHOULD (INV-039); def. INV-038 | values in its view (INV-038 with INV-003) | — | OUT-001, OUT-010, OUT-027, OUT-036 | E-037, INV-037, INV-038, INV-039 |
| OC-34 | Three-month pattern view (E-038) | OUT-028: clinicians | the three most recent calendar months or 28-day periods | every context | MUST (INV-040); def. INV-041; definitions and codes SHOULD (INV-042) | series (W2, def.) | C2-08 | OUT-028, OUT-038 | E-038, INV-040, INV-041, INV-042, INV-043 |
| OC-35 | Values per headache type (E-012, scopes `ofType`) | OUT-029: clinicians, patients | calendar month or 28-day period; intensity per period | "When the patient has, or may have, more than one headache type" — `#c.subject.possibleHeadacheTypes ≥ 2` | MUST (C1-13); intensity SHOULD where provided (C1-14); def. INV-122 | — | — | OUT-029 | E-012, INV-028, INV-029, INV-030 |
| OC-36 | Menstrual-relation view, cycle lines, attack marks (E-060, E-061) | OUT-030: clinicians, patients | consecutive cycles over the selected time range | "For patients who menstruate" — `menstruatesDuring(c, c.timeRange)` | MUST (INV-086); def. INV-087, INV-124 | attack marks (W2, def.); label; completeness | — | OUT-030, OUT-035 | E-060, E-061, INV-086, INV-087 |
| OC-37 | Cluster-headache view, cluster and remission periods, attack rates (E-062, E-063, E-064) | OUT-031: clinicians, patients | the selected time range; bouts and remissions with their own dates | "For patients with cluster headache" — `hasType(c, c3_1)` | SHOULD (INV-088); def. INV-089, INV-124 | — (no placement: fix 11 kept; CA-09) | — | OUT-031 | E-062, E-063, E-064, INV-088, INV-089 |
| OC-38 | Trigger co-occurrence view (E-065) | OUT-032: patients, clinicians | the covered period | — | MAY; def. INV-110 | caveats C3-09; label; completeness | — | OUT-001, OUT-032, OUT-038 | E-065, INV-090, INV-100 (trigger view), INV-110 |
| OC-39 | Screening result (E-059; SD-SC, SD-SR) | OUT-033: clinicians | its date | "Where results of depression or anxiety screening instruments … are available" — R-MCF (4) | SHOULD next to headache outputs (INV-083); def. INV-085 | clinical-interpretation caveat (C3-10); availability fact (INV-123) | C2-09 | OUT-033, OUT-038 | E-059, INV-083, INV-084, INV-085, INV-100 (screening) |
| OC-40 | Clinician-facing summary (E-066) | OUT-034: primary-care clinicians, neurologists, headache specialists | a period chosen by the clinician (any dates); the period since the previous consultation | clinician audiences — `c.audience ∈ Clinicians` | SHOULD (INV-094); content SHOULD (INV-104) | — | — | OUT-034, OUT-039 | E-066, INV-094, INV-104 |
| OC-41 | Patient-facing overview (E-067) | OUT-035: patients, parents and caregivers | any covered period | patient, parent and caregiver audiences | SHOULD (INV-095); content SHOULD (INV-105) | — | — | OUT-035 | E-067, INV-095, INV-105 |
| OC-42 | Paediatric outputs: PedMIDAS, school days, caregiver impact, equal-length comparisons, supportive information (E-031; with E-030, E-058) | OUT-036: parents and caregivers, paediatric clinicians, researchers | periods that begin, and results completed, while the subject is a child or adolescent | "For children and adolescents" — `childOn`, `childIn` | SHOULD (INV-096, INV-097); def. INV-121 | supportive-information caveat (C3-11) | — | OUT-036 | E-031, INV-096, INV-097, INV-098 |
| OC-43 | Composite headache index (E-033) | OUT-037: clinicians, patients, researchers | per reporting period | "For migraine" (`concerns(…, c1)`); "for tension-type headache" (`concerns(…, c2)`) | no availability; content SHOULD (INV-092, INV-093); def. INV-115 | exploratory label (C3-12); components for migraine (W2 SHOULD) | SHOULD NOT primary for migraine (INV-091) | OUT-037 | E-033, INV-091, INV-092, INV-093, INV-115 |
| OC-44 | Label or caveat (E-010) | as the element it qualifies | — | — | structural; asked by the C3 cells | shown with what it qualifies (W2, def., on `qualifies`) | — | OUT-008, OUT-011, OUT-016, OUT-017, OUT-032, OUT-036, OUT-037, OUT-038 | E-010, INV-007 |
| OC-45 | Other content (E-004 `OtherItem`) | any | — | — | permitted (section 3.7) | — | the C2 cells whose bearer is every element (C2-01, C2-02, C2-05, C2-07) | OUT-038 | E-004 |

Elements that are not outputs and have no row: E-001 (root; holds `claims`, `presents`, `factsShown`), E-007 and E-008 (context), E-009 (codes; values in SD-IC), and E-014 (abstract `DayCount`; nesting in INV-122). The Realises column of each row equals, by script, the union of the Realises fields of the items named in the row (section 14).

### 4.4 Formal columns (model section 4.4)

OMN declarations (one `omn` block at the start of model section 4.4):

```omn
enum CatalogueRow ::= oc01 | oc02 | oc03 | oc04 | oc05 | oc06 | oc07 | oc08 | oc09 | oc10 | oc11 | oc12 | oc13 | oc14 | oc15
  | oc16 | oc17 | oc18 | oc19 | oc20 | oc21 | oc22 | oc23 | oc24 | oc25 | oc26 | oc27 | oc28 | oc29 | oc30 | oc31 | oc32
  | oc33 | oc34 | oc35 | oc36 | oc37 | oc38 | oc39 | oc40 | oc41 | oc42 | oc43 | oc44 | oc45     -- ocNN names row OC-NN
fun ppGranularities(r : CatalogueRow, l : Level) : set Granularity ≙ table C1 default ∅
fun ppRequired(r : CatalogueRow, l : Level, c : OutputContext) : set (TypeScope × set (ℙ PeriodValue)) ≙ table C1 default ∅
fun prohibitedClaims(r : CatalogueRow, l : Level) : set (ℙ Claim × ℙ Element) ≙ table C2 default ∅
fun requiredAnnotations(r : CatalogueRow, l : Level) : set (AnnotationKind × ℙ Element) ≙ table C3 default ∅
```

`medicationKinds` is a new definition in E-029. It is the set of kinds of INV-023, verbatim, so that C1-10 and C1-13 name it once:

```omn
fun medicationKinds(c : OutputContext) : set (ℙ PeriodValue) ≙ {TotalAcuteMedicationDays} ∪
  {m ∈ c.subject.acuteMedications • {d : DayCount | d.measure = acuteMedicationDays(ofClass(classOf(m.drug)))}} ∪
  {m ∈ c.subject.acuteMedications • {d : DayCount | d.measure = acuteMedicationDays(ofDrug(m.drug))}}
```

**Case table C1 — cases of `ppGranularities` and `ppRequired` (per-period availability, read by INV-118).**

In the model, the "Replaces" column becomes "Stage 1 part", naming the statement part instead.

| Row | `r : CatalogueRow` | `l : Level` | `ppGranularities(r, l)` | `ppRequired(r, l, c)` | Replaces (v34) | Stage 1 part |
|---|---|---|---|---|---|---|
| C1-01 | `oc05` | `must` | `MonthlyKind` | `{(allTypes, {HeadacheDays})}` | INV-014 | OUT-001 (MUST), OUT-004 (MUST) |
| C1-02 | `oc06` | `must` | `MonthlyKind` | `{q ∈ {(allTypes, {MigraineDays})} \| hasType(c, c1)}` | INV-015 | OUT-001, OUT-005 (MUST) |
| C1-03 | `oc07` | `should` | `MonthlyKind` | `{(allTypes, {ModerateSevereHeadacheDays})}` | INV-016 | OUT-006 (SHOULD) |
| C1-04 | `oc07` | `must` | `MonthlyKind` | `{q ∈ {(allTypes, {ModerateSevereHeadacheDays})} \| provides(ModerateSevereHeadacheDays)}` | INV-108 (first measure) | OUT-001 (MUST) |
| C1-05 | `oc08` | `should` | `MonthlyKind` | `{(allTypes, {AttackCount})}` | INV-017 | OUT-007 (SHOULD) |
| C1-06 | `oc08` | `must` | `MonthlyKind` | `{q ∈ {(allTypes, {AttackCount})} \| provides(AttackCount)}` | INV-108 (second measure) | OUT-001 (MUST) |
| C1-07 | `oc11` | `should` | `Granularity` | `{(allTypes, {{m : IntensitySummary \| m.scale ≠ ∅}})}` | INV-018 | OUT-010 (SHOULD) |
| C1-08 | `oc12` | `should` | `Granularity` | `{(allTypes, {{m : DurationSummary \| m.kind ≠ auraDuration}})}` | INV-019 | OUT-011 (SHOULD) |
| C1-09 | `oc13` | `should` | `Granularity` | `{q : TypeScope × set (ℙ PeriodValue) \| hasType(c, c1) ∧ (q = (allTypes, {MostBothersomeSymptomItem}) ∨ ∃ s : AssociatedSymptom • q = (allTypes, {{m : AssociatedSymptomSummary \| m.symptom = s}}))}` | INV-022 | OUT-012 (SHOULD) |
| C1-10 | `oc15` | `must` | `Granularity` | `{(allTypes, medicationKinds(c))}` | INV-023 | OUT-014 (MUST) |
| C1-11 | `oc16` | `should` | `{calendarWeek}` | `{(allTypes, {TotalAcuteMedicationDays})}` | INV-025 | OUT-015 (SHOULD) |
| C1-12 | `oc32` | `should` | `Granularity` | `{(allTypes, {fiDays(paidWorkOrSchool, affected), fiDays(householdWork, affected), fiDays(socialOrLeisure, affected), {m : DayCount \| ∃ d : ImpactDomain • m.measure = functionalImpactDays((d, severelyImpaired))}})}` | INV-026 | OUT-027 (SHOULD) |
| C1-13 | `oc35` | `must` | `MonthlyKind` | `{q : TypeScope × set (ℙ PeriodValue) \| #c.subject.possibleHeadacheTypes ≥ 2 ∧ q.1 ∈ {allTypes} ∪ {t ∈ c.subject.possibleHeadacheTypes • ofType(t)} ∧ q.2 = {HeadacheDays} ∪ medicationKinds(c) ∪ {K ∈ {ModerateSevereHeadacheDays, AttackCount} \| provides(K)}}` | INV-028 | OUT-029 (MUST) |
| C1-14 | `oc35` | `should` | `Granularity` | `{q : TypeScope × set (ℙ PeriodValue) \| #c.subject.possibleHeadacheTypes ≥ 2 ∧ provides(IntensitySummary) ∧ q.2 = {IntensitySummary} ∧ ∃ t ∈ c.subject.possibleHeadacheTypes • q.1 = ofType(t)}` | INV-029 | OUT-029 (SHOULD, where OUT-010 is provided) |

**Case table C2 — cases of `prohibitedClaims` (read by INV-119).**

| Row | `r : CatalogueRow` | `l : Level` | `prohibitedClaims(r, l)` | Replaces (v34) | Stage 1 part |
|---|---|---|---|---|---|
| C2-01 | `oc01` | `shouldNot` | `{({x : Claim \| x = replacesClinicalAssessment ∨ ∃ d : DiagnosisRef • x = diagnosis(d)}, Element)}` | INV-101 | OUT-038 (SHOULD) |
| C2-02 | `oc04` | `shouldNot` | `{({clinicallyValidatedCutoff}, Element)}` | INV-013 | OUT-003 (SHOULD NOT) |
| C2-03 | `oc12` | `shouldNot` | `{({standAloneEfficacyMeasure}, {d : DurationSummary \| d.kind ≠ auraDuration ∧ d.attackScope ≠ untreatedAttacks})}` | INV-021 | OUT-011 Caveat (SHOULD) |
| C2-04 | `oc17` | `mustNot` | `{({x : Claim \| ∃ t : ICHD3Code • t ⊑ c8_2 ∧ x = diagnosis(headacheDiagnosis(t))}, MedicationOveruseIndicator)}` | INV-048 | OUT-016 (MUST NOT) |
| C2-05 | `oc21` | `mustNot` | `{({continuationDecision}, Element)}` | INV-106 | OUT-018 Caveat (MUST); OUT-020 Rationale (second part) |
| C2-06 | `oc23` | `shouldNot` | `{({soleIndicatorOfIndividualBenefit}, ResponderLabel)}` | INV-065 | OUT-020 (SHOULD NOT) |
| C2-07 | `oc28` | `shouldNot` | `{({acuteResponseDefinitionDecision}, Element)}` | INV-107 | OUT-023 Caveat (SHOULD) |
| C2-08 | `oc34` | `shouldNot` | `{({x : Claim \| ∃ d : DiagnosisRef • x = diagnosis(d)}, {x : Element \| x ∈ ThreeMonthPatternView ∨ ∃ v : ThreeMonthPatternView • x ∈ v.content})}` | INV-043 | OUT-028 (SHOULD NOT) |
| C2-09 | `oc39` | `shouldNot` | `{({x : Claim \| ∃ y : Text • x = diagnosis(psychiatricDiagnosis(y))}, ScreeningResult)}` | INV-084 | OUT-033 Caveat (SHOULD) |

**Case table C3 — cases of `requiredAnnotations` (read by INV-120).**

| Row | `r : CatalogueRow` | `l : Level` | `requiredAnnotations(r, l)` | Replaces (v34) | Stage 1 part |
|---|---|---|---|---|---|
| C3-01 | `oc01` | `should` | `{(patientReportedDiaryInformation, View), (supportsDoesNotReplaceClinicalAssessment, View)}` | INV-099 | OUT-038 (SHOULD) |
| C3-02 | `oc09` | `may` | `{(exploratoryMeasure, HeadacheFreeDays ∪ SymptomFreeDays ∪ MigraineFreePeriodMark)}` | — (E-010 Conformance: MAY; no constraint) | OUT-008 (MAY) |
| C3-03 | `oc12` | `should` | `{(durationInfluencedByAcuteTreatment, {d : DurationSummary \| d.kind ≠ auraDuration ∧ d.attackScope ≠ untreatedAttacks})}` | INV-020 | OUT-011 (SHOULD) |
| C3-04 | `oc17` | `must` | `{(reviewPromptPossibleMedicationOveruse, MedicationOveruseIndicator)}` | INV-047 | OUT-016 (MUST) |
| C3-05 | `oc17` | `should` | `{(requiresClinicalInterpretation, MedicationOveruseIndicator)}` | INV-100, first conjunct | OUT-038 (SHOULD) |
| C3-06 | `oc18` | `should` | `{(expectedTransientWorseningEarlyWithdrawal, WithdrawalFollowUpView)}` | INV-052 | OUT-017 (SHOULD) |
| C3-07 | `oc23` | `should` | `{(requiresClinicalInterpretation, ResponderLabel)}` | INV-100, second conjunct | OUT-038 |
| C3-08 | `oc31` | `should` | `{(requiresClinicalInterpretation, {r : InstrumentResult \| r.category ≠ ∅})}` | INV-100, fourth conjunct | OUT-038, OUT-026 |
| C3-09 | `oc38` | `should` | `{(coOccurrenceNotCausation, TriggerCooccurrenceView), (apparentTriggersMayBePremonitorySymptoms, TriggerCooccurrenceView), (requiresClinicalInterpretation, TriggerCooccurrenceView)}` | INV-090; INV-100, third conjunct | OUT-032 (caveats SHOULD), OUT-038 |
| C3-10 | `oc39` | `should` | `{(requiresClinicalInterpretation, ScreeningResult)}` | INV-100, fifth conjunct | OUT-038, OUT-033 |
| C3-11 | `oc42` | `should` | `{(supportiveInformation, {v : View \| childIn(ctx(outputOf(v)), {v.covers} ∪ (v.content ∩ Period)) ∨ ∃ r ∈ v.content ∩ InstrumentResult; d ∈ r.completionDate • childOn(ctx(outputOf(v)), d)})}` | INV-098 | OUT-036 Caveat (SHOULD) |
| C3-12 | `oc43` | `should` | `{(exploratoryMeasure, {x : CompositeIndex \| concerns(ctx(outputOf(x)), x.typeScope, c1)})}` | INV-092, first conjunct | OUT-037 (SHOULD) |

`ctx(outputOf(…))` replaces the bare `ctx` of INV-098 and INV-092, because a defined function has no output scope of its own. In an output-scope invariant, `ctx(outputOf(x))` = `ctx` for every atom x of the output (section 2.5). The two forms give the same verdict.

---

## 5. Generic invariants (model section 6.0)

All are new IDs (PROCESS.md section 7). Each Evidence field: "Stage 1 statements named in the Stage 1 part column of its table (C1, C2, C3, SD-DF), or in its Realises field".

### INV-118 Per-period values are available for every period of the selected time range

```omn
∀ r : CatalogueRow • ppGranularities(r, l) ≠ ∅ ⇒
  ∃ g ∈ ppGranularities(r, l) • ∀ c ∈ Ctx • c.granularity = g ⇒ ∀ q ∈ ppRequired(r, l, c) • reportedTogether(c, q.2, q.1)
```

- **Conformance:** level-indexed (section 3.3, item 7): MUST for the C1 cases with `l = must` (C1-01, 02, 04, 06, 10, 13), SHOULD for those with `l = should` (C1-03, 05, 07, 08, 09, 11, 12, 14). Scope: repertoire.
- **Realises:** OUT-001, OUT-004, OUT-005, OUT-006, OUT-007, OUT-010, OUT-011, OUT-012, OUT-014, OUT-015, OUT-027, OUT-029.
- **Replaces:** INV-014, 015, 016, 017, 018, 019, 022, 023, 025, 026, 028, 029, 108.
- **Equivalence.** For each C1 case, the instance unfolds to the replaced v34 predicate:
  - `reportedTogether(c, {K}, sc)` is `reportedPerPeriod(c, K, sc)` (model section 3.4).
  - A case whose `ppRequired` holds the pairs (sc, Ks) asks `reportedTogether` for each pair, as INV-022 (four separate kinds), INV-028 (each scope) and INV-029 (each type) do.
  - An applicability condition inside `ppRequired` (`hasType`, `provides`, `#possibleHeadacheTypes ≥ 2`) makes the set empty outside the condition, which is the v34 implication; `MonthlyKind`, `Granularity` and `{calendarWeek}` are non-empty.
  - Every v34 invariant that has its own `∃ g` is its own case. INV-108's two measures are two cases (C1-04, C1-06), and INV-018 and INV-029 are two cases (C1-07, C1-14); merging them under one `∃ g` would strengthen the rule (the mutation test finds it).
  - **INV-025.** v34: `∀ c • c.granularity = calendarWeek ⇒ ∃ o, v ∈ WeeklyMedicationView, sr • tiles(sr, c.timeRange, calendarWeek) ∧ perPeriod(v, sr, TotalAcuteMedicationDays, allTypes)`. C1-11 gives `∀ c • c.granularity = calendarWeek ⇒ ∃ o, v, sr • tiles(sr, c.timeRange, c.granularity) ∧ perPeriod(…)`. A witness `sr` with `tiles(…, calendarWeek)` has granularity `calendarWeek` (E-006 `tiles`), so v is a `WeeklyMedicationView` (E-036); the converse is immediate. E-036 stays as the output kind of OC-16.
- **Check:** `eq_g1.py`: 0 mismatches in 200,000 models, per level.

### INV-119 No element is presented with a prohibited claim

```omn
¬ ∃ x : Element; r : CatalogueRow; q ∈ prohibitedClaims(r, l) • x ∈ q.2 ∧ ∃ C ∈ q.1 • presents(x, C)
```

New in E-001:

```omn
pred presents(x : Element, C : Claim) ≙ C ∈ x.claims ∨ ∃ a : Annotation • x ∈ a.qualifies ∧ C ∈ a.claims
```

- **Conformance:** level-indexed: SHOULD NOT for the C2 cases with `l = shouldNot`, MUST NOT for those with `l = mustNot` (C2-04, C2-05). Scope: output.
- **Realises:** OUT-003, OUT-011, OUT-016, OUT-018, OUT-020, OUT-023, OUT-028, OUT-033, OUT-038.
- **Replaces:** INV-013, 021, 043, 048, 065, 084, 101, 106, 107.
- **Equivalence.**
  - Where the bearer is every element (C2-01, 02, 05, 07), the annotation disjunct of `presents` adds nothing, because the annotation is itself a bearer.
  - For C2-08 (three-month view), annotations qualifying the view or its items are in the view's content (INV-007, now rule W2 on `qualifies`), so they are bearers.
  - C2-04 and C2-09 had the annotation disjunct in v34 (INV-048, INV-084).
  - For C2-03 and C2-06 the disjunct is new: **CHG-07** (section 12).
  - INV-043 and INV-084 are also implied by C2-01 at the same level; the redundant cells are kept so that OUT-028 and OUT-033 trace to them.
- **Check:** `eq_g2g3.py`: MUST NOT 0 mismatches; SHOULD NOT 349 differences in 100,000 models, all explained by CHG-07.

### INV-120 Required labels and caveats are shown

```omn
∀ x : Element; r : CatalogueRow; q ∈ requiredAnnotations(r, l) • x ∈ q.2 ⇒ annotated(x, q.1)
```

- **Conformance:** level-indexed: MUST for C3-04; SHOULD for the other cases with `l = should`; the `may` case (C3-02) imposes nothing. Scope: output.
- **Realises:** OUT-008, OUT-011, OUT-016, OUT-017, OUT-020, OUT-026, OUT-032, OUT-033, OUT-036, OUT-037, OUT-038.
- **Replaces:** INV-020, 047, 052, 090, 098, 099, 100, and the conjunct `annotated(x, exploratoryMeasure)` of INV-092.
- **Equivalence:** each case is the replaced conjunct with its bearer set.
- **Check:** `eq_g2g3.py`, 0 mismatches.

### INV-121 Values within their period (definitional)

New in E-012:

```omn
fun daysWithin(x : PeriodValue) : set ℕ ≙
  {m ∈ {x} ∩ DayCount • m.days} ∪
  {n : ℕ | ∃ ci ∈ {x} ∩ CompletenessIndicator • coveredDays(n) ∈ ci.expressions} ∪
  {n : ℕ | ∃ i ∈ {x} ∩ IntensitySummary; ds : set1 LevelDays • i.summary = peakIntensityDistribution(ds) ∧ ∃ ld ∈ ds • ld.days = n} ∪
  {n : ℕ | ∃ a ∈ {x} ∩ AssociatedSymptomSummary • a.presence = daysWithSymptom(n)} ∪
  {n : ℕ | ∃ ci ∈ {x} ∩ CaregiverImpact • ci.impact = caregiverLostProductiveDays(n)}
```

Predicate:

```omn
(∀ x : PeriodValue; n ∈ daysWithin(x) • n ≤ x.period.lengthDays) ∧
(∀ d : DurationSummary • d.kind = moderateSeverePainTime ∧ d.statistic = total ⇒ d.value ≤ daysLong(d.period.lengthDays))
```

- **Conformance:** definitional (E-012, E-013, E-014, E-023, E-024, E-025, E-031). Scope: output.
- **Realises:** OUT-001, OUT-003, OUT-004, OUT-005, OUT-006, OUT-008, OUT-010, OUT-011, OUT-012, OUT-014, OUT-015, OUT-027, OUT-036.
- **Replaces:**
  - INV-005 (whole);
  - INV-012: `(∀ n : ℕ • coveredDays(n) ∈ ci.expressions ⇒ n ≤ ci.period.lengthDays)`;
  - INV-032: `(∀ ld ∈ ds • ld.days ≤ i.period.lengthDays)`;
  - INV-033: the moderate/severe pain-time conjunct, the `daysWithSymptom` conjunct and the caregiver conjunct.
- **Equivalence:** by unfolding `daysWithin` (one union member per replaced conjunct).

### INV-122 Nested day counts do not exceed the counts that contain them (definitional)

New in E-014:

```omn
pred nestedIn(k₁ : DayMeasure, k₂ : DayMeasure) ≙
  (k₁ = moderateSevereHeadacheDays ∧ k₂ = headacheDays) ∨
  (k₁ = symptomFreeDays ∧ k₂ = headacheFreeDays) ∨
  (∃ k : AcuteDrugClass • k₁ = acuteMedicationDays(ofClass(k)) ∧ k₂ = acuteMedicationDays(allAcuteMedication)) ∨
  (∃ dr ∈ dom classOf • k₁ = acuteMedicationDays(ofDrug(dr)) ∧ k₂ = acuteMedicationDays(ofClass(classOf(dr)))) ∨
  (∃ ks : set1 AcuteDrugClass; k ∈ ks • k₁ = acuteMedicationDays(ofClass(k)) ∧ k₂ = acuteMedicationDays(ofClasses(ks))) ∨
  (∃ ks : set1 AcuteDrugClass • k₁ = acuteMedicationDays(ofClasses(ks)) ∧ k₂ = acuteMedicationDays(allAcuteMedication)) ∨
  (∃ d : ImpactDomain; s ∈ {missed, impaired, severelyImpaired} • k₁ = functionalImpactDays((d, s)) ∧ k₂ = functionalImpactDays((d, affected)))
```

Predicate (the last two conjuncts are INV-030, verbatim):

```omn
(∀ v : View; p : Period; sc : TypeScope; k₁, k₂ : DayMeasure • nestedIn(k₁, k₂) ⇒
   ∀ a ∈ daysOf(v, k₁, p, sc); b ∈ daysOf(v, k₂, p, sc) • a ≤ b) ∧
(∀ v : View; p : Period; h : HeadacheType; k : DayMeasure •
   (k ∈ {headacheDays, migraineDays, moderateSevereHeadacheDays} ∨ k is acuteMedicationDays) ⇒
     ∀ a ∈ daysOf(v, k, p, ofType(h)); b ∈ daysOf(v, k, p, allTypes) • a ≤ b) ∧
(∀ v : View • ∀ e, f ∈ v.content ∩ EventCount • e.event = f.event ∧ sameSpan(e.period, spanOf(f.period)) ∧
   (∃ h : HeadacheType • e.typeScope = ofType(h)) ∧ f.typeScope = allTypes ⇒ e.count ≤ f.count)
```

- **Conformance:** definitional (E-012, E-014, E-017, E-019, E-021, E-029, E-030). Scope: output.
- **Realises:** OUT-006, OUT-008, OUT-014, OUT-016, OUT-027, OUT-029.
- **Replaces:**
  - INV-030 (whole);
  - INV-024: its first conjunct (class ≤ total), its second (drug ≤ class), and the first two parts of its third (class ≤ basis of a set of classes; basis ≤ total);
  - INV-031: `a ≤ b` for moderate/severe ≤ headache days and for symptom-free ≤ headache-free days;
  - INV-033: the functional-impact conjunct.
- **Equivalence:** one disjunct of `nestedIn` per replaced conjunct, with the same quantifier ranges.
- **Check:** `eq_misc.py`, 0 mismatches in 100,000 models.

### INV-123 Facts of the context that an output shows are facts the context states (definitional)

New in E-008:

```omn
variant ShownFact ::= preventiveCourse ⟨Treatment⟩ | acuteCourse ⟨Treatment⟩ | courseEvent ⟨CourseEvent⟩
  | stopOn ⟨Treatment × Date⟩ | stoppedCourse ⟨Treatment⟩ | withdrawal ⟨Date⟩
  | usedMedication ⟨Drug × set FormulationOrRoute⟩ | usedScope ⟨MedicationScope⟩
  | availableResult ⟨Instrument × set Date⟩ | availableScreening ⟨ScreeningInstrument × set Date⟩
pred inMedicationScope(m : AcuteMedication, s : MedicationScope) ≙ s = allAcuteMedication ∨ s = ofClass(classOf(m.drug)) ∨
  s = ofDrug(m.drug) ∨ (∃ ks : set1 AcuteDrugClass • s = ofClasses(ks) ∧ classOf(m.drug) ∈ ks)
pred stated(c : OutputContext, f : ShownFact) ≙
  (∀ t : Treatment • f = preventiveCourse(t) ⇒ t ∈ c.subject.preventiveTreatments) ∧
  (∀ t : Treatment • f = acuteCourse(t) ⇒ t ∈ c.subject.acuteTreatments) ∧
  (∀ e : CourseEvent • f = courseEvent(e) ⇒ e ∈ c.subject.courseEvents) ∧
  (∀ t : Treatment; d : Date • f = stopOn((t, d)) ⇒ ∃ k : StopKind • eventOn(c, t, stop(k), d)) ∧
  (∀ t : Treatment • f = stoppedCourse(t) ⇒ stopped(c, t)) ∧
  (∀ d : Date • f = withdrawal(d) ⇒ d ∈ c.subject.withdrawalStart) ∧
  (∀ dr : Drug; fs : set FormulationOrRoute • f = usedMedication((dr, fs)) ⇒
     ∃ m ∈ c.subject.acuteMedications • m.drug = dr ∧ ∀ x ∈ fs • m.formulation = x) ∧
  (∀ s : MedicationScope • f = usedScope(s) ⇒ ∃ m ∈ c.subject.acuteMedications • inMedicationScope(m, s)) ∧
  (∀ i : Instrument; ds : set Date • f = availableResult((i, ds)) ⇒ (∃ a ∈ c.subject.instrumentAdministrations • a.instrument = i) ∧
     ∀ d ∈ ds • InstrumentAdministration(instrument ↦ i, date ↦ d) ∈ c.subject.instrumentAdministrations) ∧
  (∀ i : ScreeningInstrument; ds : set Date • f = availableScreening((i, ds)) ⇒ (∃ a ∈ c.subject.screeningAdministrations • a.instrument = i) ∧
     ∀ d ∈ ds • ScreeningAdministration(instrument ↦ i, date ↦ d) ∈ c.subject.screeningAdministrations)
```

New in E-001 (the facts each kind of element shows):

```omn
fun factsShown(x : Element) : set ShownFact ≙
  {mk ∈ {x} ∩ TreatmentMarker • preventiveCourse(mk.treatment)} ∪
  {mk ∈ {x} ∩ TreatmentMarker • courseEvent(CourseEvent(treatment ↦ mk.treatment, kind ↦ mk.event, date ↦ mk.date))} ∪
  {rc ∈ {x} ∩ ResponseComparison • preventiveCourse(rc.treatment)} ∪
  {rc ∈ {x} ∩ ResponseComparison • courseEvent(CourseEvent(treatment ↦ rc.treatment, kind ↦ start, date ↦ rc.treatmentStart))} ∪
  {a ∈ {x} ∩ AdherenceSummary • preventiveCourse(a.treatment)} ∪
  {v ∈ {x} ∩ TreatmentReviewView • preventiveCourse(v.treatment)} ∪
  {v ∈ {x} ∩ PostStopMonitoringView • preventiveCourse(v.treatment)} ∪
  {v ∈ {x} ∩ PostStopMonitoringView • courseEvent(CourseEvent(treatment ↦ v.treatment, kind ↦ v.event, date ↦ v.eventDate))} ∪
  {L ∈ {x} ∩ ResponderLabel • preventiveCourse(L.treatment)} ∪
  {v ∈ {x} ∩ WithdrawalFollowUpView • withdrawal(v.withdrawalStart)} ∪
  {l ∈ {x} ∩ TreatedAttackLine • usedMedication((l.drug, l.formulation))} ∪
  {l ∈ {x} ∩ TreatmentLine | l.role = preventive • preventiveCourse(l.treatment)} ∪
  {l ∈ {x} ∩ TreatmentLine | l.role = acute • acuteCourse(l.treatment)} ∪
  {f : ShownFact | ∃ l ∈ {x} ∩ TreatmentLine; s ∈ l.startDate • f = courseEvent(CourseEvent(treatment ↦ l.treatment, kind ↦ start, date ↦ s))} ∪
  {f : ShownFact | ∃ l ∈ {x} ∩ TreatmentLine; e ∈ l.stopDate • f = stopOn((l.treatment, e))} ∪
  {f : ShownFact | ∃ l ∈ {x} ∩ TreatmentLine; dc ∈ l.doseChanges •
     f = courseEvent(CourseEvent(treatment ↦ l.treatment, kind ↦ doseChange(dc.direction), date ↦ dc.date))} ∪
  {l ∈ {x} ∩ TreatmentLine | l.stopReason ≠ ∅ • stoppedCourse(l.treatment)} ∪
  {f : ShownFact | ∃ l ∈ {x} ∩ TreatmentLine; fo ∈ l.formulations • l.role = acute ∧ f = usedMedication((l.drug, {fo}))} ∪
  {f : ShownFact | ∃ m ∈ {x} ∩ DayCount; s : MedicationScope • m.measure = acuteMedicationDays(s) ∧ m.days > 0 ∧ f = usedScope(s)} ∪
  {r ∈ {x} ∩ InstrumentResult • availableResult((r.instrument, r.completionDate))} ∪
  {r ∈ {x} ∩ ScreeningResult • availableScreening((r.instrument, r.date))}
```

Predicate:

```omn
∀ x : Element; f ∈ factsShown(x) • stated(ctx, f)
```

- **Conformance:** definitional (E-008 and the elements named in `factsShown`). Scope: output.
- **Realises:** OUT-009, OUT-012, OUT-014, OUT-016, OUT-017, OUT-018, OUT-020, OUT-021, OUT-022, OUT-023, OUT-024, OUT-026, OUT-033, OUT-036, OUT-039.
- **Replaces** (conjuncts quoted from v34):
  - INV-036 (whole). Its conjunct `markedKind(mk.event)` moves into E-034's attribute type (section 8).
  - INV-113 (whole).
  - INV-117 (whole).
  - INV-056: `rc.treatment ∈ ctx.subject.preventiveTreatments ∧ rc.treatmentStart ∈ startOf(ctx, rc.treatment)` (from MUST to definitional: CHG-R1).
  - INV-067: `a.treatment ∈ ctx.subject.preventiveTreatments`.
  - INV-068: `v.treatment ∈ ctx.subject.preventiveTreatments` (from MUST to definitional: CHG-R1).
  - INV-075: `(∃ m ∈ ctx.subject.acuteMedications • m.drug = l.drug ∧ ∀ f ∈ l.formulation • m.formulation = f)`.
  - INV-079: the two role conjuncts, the start-date, stop-date, dose-change and stop-reason conjuncts, and the formulation conjunct.
  - INV-082: its last two conjuncts (availability).
  - INV-085: its last two conjuncts (availability).
  - INV-112: `v.treatment ∈ ctx.subject.preventiveTreatments ∧ … ∧ eventOn(ctx, v.treatment, v.event, v.eventDate)`. Its conjunct `(v.event is stop ∨ v.event = doseChange(reduction))` moves into E-049's attribute type (section 8).
- **New (CHG-05, CA-03):** the `usedScope` facts of acute-medication day counts above 0.
- **Equivalence** (for all but the `usedScope` member):
  - `rc.treatmentStart ∈ startOf(ctx, t)` ⇔ `CourseEvent(t, start, rc.treatmentStart) ∈ ctx.subject.courseEvents` (definition of `startOf`).
  - `eventOn` is membership of the course event.
  - `AcuteMedication(drug ↦ l.drug, formulation ↦ f) ∈ acuteMedications` ⇔ `∃ m • m.drug = l.drug ∧ m.formulation = f` (value equality).
  - The role conjuncts `(role = preventive ⇔ t ∈ preventive) ∧ (role = acute ⇔ t ∈ acute)` equal the two role facts, because INV-001 makes the two sets disjoint (`eq_misc.py`, all cases).
- **Class.** The class of this rule is: every attribute whose value names an entity of the subject's profile, or presupposes an event of it. Its members are the 13 element kinds in `factsShown`. Three attributes of the class are tied elsewhere, by rules that also do more:
  - E-042 `treatment`, `anchorDate` by INV-058 (`applicable`, `anchorDates`);
  - E-056 by INV-080 (a selection of the context);
  - E-063 `end` by INV-089 (the as-of date).
  
  `RATIONALE.md` entry INV-123/D01 holds fix 32's attribute table, updated to v35 IDs. A future fix that finds a new attribute of the class adds a member to `factsShown` (PROCESS.md section 6a).

### INV-124 The dated phases that one output shows describe one history (definitional)

New in E-060:

```omn
fun shownDayOnes(cl : CycleLine) : set Date ≙ cl.firstDayOfMenstruation ∪ {d : Date | cl.complete ∧ d = next(cl.cycle.to)}
```

(the first day of menstruation a line shows: its day 1, and, for a line that has ended, the first day of the next menstruation, E-060).

Predicate:

```omn
(∀ cl, cl₂ : CycleLine • ∀ d ∈ shownDayOnes(cl₂) • ¬ (cl.cycle.from < d ∧ d ≤ cl.cycle.to)) ∧
(∀ x, y : ClusterPhaseItem • (x ∈ RemissionPeriodItem ⇔ y ∈ RemissionPeriodItem) ⇒
   ∀ xs ∈ x.start; xe ∈ lastDay(x); ys ∈ y.start; ye ∈ lastDay(y) • (xs = ys ∧ xe = ye) ∨ xe < ys ∨ ye < xs) ∧
(∀ b : ClusterPeriodItem; r : RemissionPeriodItem • ∀ bs ∈ b.start; be ∈ lastDay(b); rs ∈ r.start; re ∈ lastDay(r) • be < rs ∨ re < bs)
```

- **Conformance:** definitional (E-060, E-063). Scope: output.
- **Realises:** OUT-030, OUT-031, OUT-035.
- **Replaces:** INV-089's conjunct `(∀ b ∈ ran v.bouts; r ∈ ran v.remissions • ∀ bs ∈ b.start; be ∈ lastDay(b); rs ∈ r.start; re ∈ lastDay(r) • be < rs ∨ re < bs)`, which the third conjunct implies (output-wide instead of within one cluster view).
- **New:**
  - CHG-01: the first conjunct, which resolves R35-01 (section 10).
  - CHG-02: the second conjunct, and the output-wide scope of the third.

### INV-125 Labels whose definition Stage 1 fixes

New in E-011:

```omn
fun fixedDefinition : LabelledMeasure ⇸ PublishedDefinition
fun fixedDefinitionLevel : LabelledMeasure ⇸ Level
axiom table SD-DF
```

Predicate:

```omn
∀ lb : DefinitionLabel • lb.measure ∈ dom fixedDefinition ∧ fixedDefinitionLevel(lb.measure) = l ⇒ lb.definition = fixedDefinition(lb.measure)
```

- **Conformance:** level-indexed: MUST for SD-DF-01, SHOULD for SD-DF-02. Scope: output.
- **Realises:** OUT-004, OUT-007.
- **Replaces:** INV-009 (MUST), INV-010 (SHOULD).
- **Equivalence:** each SD-DF row unfolds to one of the two v34 predicates.

### Rule W2: the placement markers (no new invariant ID)

Every placement conjunct below moves to a marker on the attribute it concerns. Each row is equivalent to the conjunct it replaces: same atoms, same condition, same level.

| Element.attribute | Marker | Replaces (v34 conjunct, verbatim) | Level as in v34 |
|---|---|---|---|
| E-010 `qualifies` | `shown` | INV-007 (whole): `∀ e ∈ a.qualifies • e = viewOf(a) ∨ e ∈ viewOf(a).content` | definitional |
| E-033 `components` | `shown SHOULD when concerns(ctx, self.typeScope, c1)` | INV-092: `(∀ m ∈ x.components • m ∈ viewOf(x).content)` | SHOULD |
| E-035 `series` | `shown SHOULD` | INV-035: `v.series ∈ v.content` | SHOULD |
| E-035 `markers` | `shown SHOULD` | INV-035: `(∀ mk ∈ v.markers • mk ∈ v.content)` | SHOULD |
| E-038 `series` | `shown` | INV-041: `v.series ∈ v.content` | definitional |
| E-039 `series` | `shown SHOULD` | INV-050: `sr ∈ v.content` (inside `∀ sr ∈ v.series`) | SHOULD |
| E-040 `reference`, `compared` | `shown MUST when ofResponseComparison(self)` | INV-054 (whole) | MUST |
| E-043 `timePoints` | `shown MUST` | INV-059: `tp ∈ viewOf(rc).content` | MUST |
| E-046 `comparison` | `shown SHOULD` | INV-062: `rc ∈ viewOf(L).content` (inside `∃ rc ∈ L.comparison`; `comparison` is `opt`, so `∃ rc • P ∧ Q` ≡ `(∀ rc • P) ∧ ∃ rc • Q`, as oscillation check 32 found for INV-114) | SHOULD |
| E-046 `residual` | `shown SHOULD` | INV-062: `(∀ rb ∈ L.residual • rb ∈ viewOf(L).content)` | SHOULD |
| E-046 `otherValues` | `shown SHOULD` (no marker `when`; the attribute keeps its own) | INV-062: `(∀ x ∈ L.otherValues • x ∈ viewOf(L).content)` | SHOULD |
| E-051 `outcomes`, `sequence` | `shown SHOULD` | INV-072: `(∀ os ∈ s.outcomes • os ∈ viewOf(s).content) ∧ (∀ l ∈ ran s.sequence • l ∈ viewOf(s).content)` | SHOULD |
| E-054 `preventiveGroups`, `acuteGroups` | `shown SHOULD` | INV-078: `g ∈ v.content` | SHOULD |
| E-055 `preventiveResponse`, `acuteResponse`, `adherence` | `shown SHOULD` | INV-109: `(∀ r ∈ l.preventiveResponse • r ∈ viewOf(l).content) ∧ (∀ s ∈ l.acuteResponse • s ∈ viewOf(l).content)` and `a ∈ viewOf(l).content` | SHOULD |
| E-060 (`CycleLine`) `attacks` | `shown` | INV-087: `a ∈ viewOf(cl).content` | definitional |

Not marked, deliberately:
- `ClassGroup.lines`: INV-078 keeps `l ∈ v.content`, a placement in the history view through its groups, not a direct reference.
- `MenstrualRelationView.cycles`: INV-087 keeps `v.content ∩ CycleLine = ran v.cycles`, an equality.
- The cluster view's `bouts`, `remissions`, `rates`, `acute`: fix 11 declined their placement; CA-09, section 10.
- The references to periods: INV-003 already states them for all.

---

## 6. Source data tables (model section 11)

Each table is a case table (section 2.11) with informative columns `Row`, `Source` and `Rationale` (the entry IDs that hold the quotes). **Every formal cell is the v34 term, character for character** (white space aside). The author generates each table by script from the v34 `omn` axiom it replaces, and the checker parses it back and compares. The replaced axiom or constant definition is deleted from the element's `omn` block. The element keeps its type declarations, the predicates and functions that use the values, and one line `axiom table SD-…` or `const … ≙ table SD-…`.

| Table | Form and declarations | Rows (ID ↔ key, v34 order) | Replaces in v34 | Rationale per row |
|---|---|---|---|---|
| **SD-IC** ICHD-3 code labels | C (given): `` `k : ICHD3Code` `` and `` `label(k)` ``; E-009 keeps `given ICHD3Code`, the `fun` declarations, the `const` declaration of the 15 codes and the two hierarchy axioms, plus `axiom table SD-IC` | SD-IC-01 `c1`, 02 `c1_2`, 03 `c1_3`, 04 `c2`, 05 `c2_3`, 06 `c3_1`, 07 `c8_2`, 08 `c8_2_1`, 09 `c8_2_2`, 10 `c8_2_3`, 11 `c8_2_4`, 12 `c8_2_5`, 13 `c8_2_6`, 14 `c8_2_7`, 15 `c8_2_8` | E-009 axiom `label(c1) = … ∧ … label(c8_2_8) = …` | 01–05: E-009/Q01 (p. 8); 06: E-009/Q02 (p. 9); 07–15: E-009/Q03 (p. 12) |
| **SD-DF** definitions that Stage 1 fixes | C (given, ⇸): `` `k : LabelledMeasure` ``, `` `fixedDefinition(k)` ``, `` `fixedDefinitionLevel(k)` `` | SD-DF-01 `headacheDaysMeasure`: `ichd3HeadacheDays`, `must`; SD-DF-02 `attacksMeasure`: `ichd3FrequencyOfAttacks`, `should`; other keys: no row | INV-009, INV-010 | Stage 1 OUT-004, OUT-007 (statement wording) |
| **SD-CLS** acute drug classes | C (given): `` `k : AcuteDrugClass` ``, `` `classCode(k)` ``, `` `overuseLevel(ofClassUse(k))` `` | SD-CLS-01 `ergotamine`: `c8_2_1`, `10`; 02 `triptans`: `c8_2_2`, `10`; 03 `nonOpioidAnalgesics`: `c8_2_3`, `15`; 04 `opioids`: `c8_2_4`, `10`; 05 `combinationAnalgesics`: `c8_2_5`, `10`; 06 `otherMedication`: `c8_2_8`, `10` | E-028 `classCode` axiom; E-032 `overuseLevel` axiom except `combinedUse`. The v34 form `∀ k ≠ nonOpioidAnalgesics • … = 10` becomes six explicit rows (AcuteDrugClass has exactly six constants, so the two are equivalent) | codes: E-009/Q03; levels: E-032/Q01 (8.2), Q02 (8.2.1), Q03 (8.2.2), Q04 (8.2.3), Q05 (8.2.4), Q06 (8.2.5), Q07 (8.2.8) |
| **SD-CMB** combined use (8.2.6) | C (given), key `` `k : OveruseScope` `` with the single key `combinedUse`; `` `overuseCode(k)` ``, `` `overuseLevel(k)` ``, `` `basisScope(k)` `` | SD-CMB-01 `combinedUse`: `c8_2_6`, `10`, `ofClasses(classesOf826)` | the `combinedUse` parts of the two E-032 axioms. The general part `∀ k : AcuteDrugClass • overuseCode(ofClassUse(k)) = classCode(k) ∧ basisScope(ofClassUse(k)) = ofClass(k)` stays in E-032 (a rule, not data) | E-028/Q02 (8.2.6 criterion B), E-028/Q03 (note 2) |
| **SD-FX** fixed numbers | V-like (constants with type and value): `` `k` ``, `` `type` ``, `` `value` ``; each row denotes `const k : type ≙ value`. An informative column `Unit` takes the v34 comment | SD-FX-01 `windowDaysBefore : ℕ ≙ 2`; 02 `windowDaysAfter : ℕ ≙ 2`; 03 `reviewWindowFromWeeks : ℕ₁ ≙ 4`; 04 `reviewWindowToWeeks : ℕ₁ ≙ 8`; 05 `followUpMonths : ℕ₁ ≙ 12`; 06 `overuseSpanMonths : ℕ₁ ≙ 3`; 07 `remissionMoreThanMonths : ℕ₁ ≙ 3`; 08 `shortestMonthlyDays : ℕ₁ ≙ 28` | the `const` lines of E-060, E-039, E-032, E-063, E-042 | 01–02: E-060/Q01, Q02; 03–05: Stage 1 OUT-017 (statement); 06: E-032/Q01–Q07; 07: E-063/Q01; 08: Stage 1 OUT-001 (statement) |
| **SD-ER** evaluation rules | V: constants of `EvaluationRule`, collected in `evaluationRules`; columns `` `k` ``, `` `guidance` ``, `` `headacheType` ``, `` `ages` ``, `` `appliesTo` ``, `` `excludes` ``, `` `anchor` ``, `` `timing` ``, `` `minOffset` ``, `` `maxOffset` ``. E-041 keeps `allPreventiveTypes`, the value type, `shift` and its axiom, and the predicates | SD-ER-01 `ruleNice1327`, 02 `ruleNice1328`, 03 `ruleNice1329`, 04 `ruleAan14A`, 05 `ruleAan14B`, 06 `ruleSignTitrated`, 07 `ruleSignFixedDose`, 08 `ruleEhf2022Q3`, 09 `ruleIhsQ2Oral`, 10 `ruleIhsQ2Monthly`, 11 `ruleIhsQ2Quarterly`, 12 `ruleNvnTitrated`, 13 `ruleRu71`, 14 `ruleRu33Bta`, 15 `ruleRuChildren`, 16 `ruleTrBox8`, 17 `ruleTr3639`, 18 `ruleTr73` | E-041 `const rule…`, its axiom, and `const evaluationRules ≙ {…}` | see the E-041 entry table below |
| **SD-RC** named responder criteria | V: constants of `ResponderCriterion`, collected in `namedCriteria`; columns `` `k` ``, `` `name` ``, `` `components` `` (the v34 set term; `<br>` between members allowed), `` `alsoRestsOn` `` | SD-RC-01 `critNice1328`, 02 `critNice1329`, 03 `critIhsQ6`, 04 `critIhs2025`, 05 `critDmkg`, 06 `critRu71` | E-045 `const crit…`, its axiom, and `const namedCriteria ≙ {…}` | E-045/Q00 (Stage 1 fragments: NICE, DMKG, Russian 7.1); 03: E-045/Q01, Q02; 04: E-046/Q01–Q05 |
| **SD-CL** control levels of the IHS position statement 2025 | C (defined), key `` `k : ControlLevel` ``; `` `inControlRange(k, n)` `` (formula cell, parameter n : ℕ), `` `controlMinMonths(k)` ``, `` `forcedAbove(k)` ``. New declarations in E-046: `pred inControlRange(k : ControlLevel, n : ℕ) ≙ table SD-CL`, `fun controlMinMonths(k : ControlLevel) : set ℕ₁ ≙ table SD-CL default ∅`, `fun forcedAbove(k : ControlLevel) : set ℕ ≙ table SD-CL default ∅` | SD-CL-01 `migraineFreedom`: `n = 0`, —, —; 02 `optimalControl`: `n < 4`, `{3}`, —; 03 `modestControl`: `4 ≤ n ∧ n ≤ 6`, —, —; 04 `insufficientControl`: `true`, —, `{6}` | the numbers inside INV-064 (`n = 0`, `#L.evaluated ≥ 3 ∧ … n < 4`, `4 ≤ n ∧ n ≤ 6`, `n > 6`), verbatim as cells | E-046/Q01 (freedom), Q02 (optimal), Q03 (modest), Q04 (insufficient), Q05 (fewer than six) |
| **SD-IN** instruments | C (given): key `` `k : Instrument` ``; `` `instrumentName(k)` ``, `` `publishedRecall(k)` `` (⇸), `` `scoreRange(k)` `` (⇸), `` `publishedGrading(k)` `` (total; `—` = not fixed) | SD-IN-01 `midas`, 02 `hit6`, 03 `msq21`, 04 `halt90`, 05 `halt30`, 06 `hurt`, 07 `mtoq`, 08 `pedmidas`, 09 `pgic`. Cells as v34: names "MIDAS", "HIT-6", "MSQ v2.1", "HALT-90", "HALT-30", "HURT", "M-TOQ", "PedMIDAS", "PGIC"; recall `recallMonths(3)` for 01, 04, 08 and `recallMonths(1)` for 02, 05, other — ; ranges `ScoreRange(low ↦ 0, high ↦ ∅)` for 01, 04, 05, 08 and `ScoreRange(low ↦ 36, high ↦ {78})` for 02, other — ; grading `true` for 01, 02, 04, 06, 08, `false` for 05, — for 03, 07, 09 | the E-057 axioms on `instrumentName` (named instruments), `publishedRecall`, `scoreRange`, `publishedGrading`. Stays in E-057: `OtherInstrumentName`, the `otherInstrument` name axiom, `wholeNumberScores`, `GradeBand`, `inBand`, `banded` and its axiom | 01: E-057/Q03, Q04, Q10; 02: E-057/Q00, Q01, Q02, Q10; 04: Q06, Q08, Q09, Q10; 05: Q00, Q07, Q08, Q10; 06: Q00; 08: Q00, Q05, Q10; 03, 07, 09: Stage 1 OUT-026 (names) |
| **SD-GB** grade bands | M: members of `const gradeBands : set1 GradeBand`; columns `` `instrument` ``, `` `grade` ``, `` `label` ``, `` `low` ``, `` `strictLow` ``, `` `high` `` | SD-GB-01 … 16, in v34 order (MIDAS I–IV, HIT-6 ×4, PedMIDAS ×4, HALT-90 I–IV) | E-057 `const gradeBands ≙ {…}` | 01–04: E-057/Q03; 05–08: Q02; 09–12: Q05; 13–16: Q09 |
| **SD-SC** screening instrument names | C (given): key `` `k : ScreeningInstrument` ``; `` `screeningName(k)` `` | SD-SC-01 `hads` "HADS", 02 `phq9` "PHQ-9", 03 `gad7` "GAD-7" | E-059 `screeningName` axiom for the three (the `otherScreeningInstrument` part stays) | Stage 1 OUT-033 (names) |
| **SD-SR** screening score ranges | C (given, ⇸): keys `` `i : ScreeningInstrument` ``, `` `s : Subscale` ``; `` `screeningMax(i, s)` ``. New declaration in E-059: `fun screeningMax : ScreeningInstrument × Subscale ⇸ ℕ` and `axiom table SD-SR` | SD-SR-01 (`hads`, `anxietySubscale`) `21`; 02 (`hads`, `depressionSubscale`) `21`; 03 (`phq9`, `wholeScale`) `27`; 04 (`gad7`, `wholeScale`) `21` | the numbers inside INV-085 | 01–02: E-059/Q01; 03: E-059/Q02; 04: E-059/Q03 |
| **SD-ET** early time points | C (defined): key `` `k : EarlyTimePoint` ``; `` `earlyTimePointType(k)` ``. New declaration in E-050: `fun earlyTimePointType(k : EarlyTimePoint) : set ICHD3Code ≙ table SD-ET default ∅` | SD-ET-01 `fifteenMinutes`: `{c3_1}`; SD-ET-02 `twoHours`: `∅` (the time point of every other summary, INV-073) | the constants inside INV-073 | Stage 1 OUT-023 ("For cluster headache, the corresponding time point is 15 minutes"), OUT-031 |

**E-041 Evidence → entries → SD-ER rows.** Q00 is the lead paragraph of E-041 Evidence; Qnn is its n-th bullet, in v34 order.

| Entry | v34 bullet (first words) | SD-ER rows |
|---|---|---|
| E-041/Q00 | lead: "Stage 1 OUT-018; OUT-036 (d) … The offsets of eleven rules are in Stage 1 quotes …" | 01, 02, 03, 04, 06, 07, 08, 10, 11, 12, 13 (offsets) and the headache type of all rows |
| Q01 | [S-015] "This guideline covers …" | 01–03 (ages) |
| Q02 | [S-015] headings "Migraine with or without aura" … | 01–03 |
| Q03 | [S-015] "For CGRP inhibitors …" (1.3.24) | 02 (ages) |
| Q04 | [S-015] "Intramuscular injection of botulinum toxin type A …" (1.3.26) | 03 (ages) |
| Q05 | [S-018] "This is a summary of the American Academy of Neurology …" | 04, 05 (ages) |
| Q06 | [S-018] "14B. …" | 05 |
| Q07 | [S-018] "14H. …" | 04 (excludes) |
| Q08 | [S-016] "This guideline provides recommendations …" | 06, 07 (ages) |
| Q09 | [S-016] "Studies of children with migraine were not included …" | 06, 07 (ages) |
| Q10 | [S-011] "In 2019 the European Headache Federation …" | 08 (ages) |
| Q11 | [S-011] "Considering the new knowledge …" | 08 (ages) |
| Q12 | [S-008] "In individuals initiating a new migraine oral preventive treatment …" (Optimal) | 09 |
| Q13 | [S-008] "In individuals initiating a new oral preventive treatment …" (Essential) | 09 |
| Q14 | [S-008] headings Q2 and Q13 | 09–11 (ages) |
| Q15 | [S-028] "P: Patiënten (kinderen en volwassenen) …" | 12 (ages) |
| Q16 | [S-033] "Возрастная категория: взрослые" | 13, 14 (ages) |
| Q17 | [S-033] "при отсутствии эффекта в течение 3 месяцев …" | 14; 13 (excludes) |
| Q18 | [S-033] "Рекомендуется для профилактики хронической М …" | 14 (type) |
| Q19 | [S-034] "назначение препаратов …" | 15 |
| Q20 | [S-034] "Возрастная группа" … "дети" | 15 (ages) |
| Q21 | [S-034] "Диагностика мигрени у детей и подростков …" | 15 (ages) |
| Q22 | [S-035] "Yeterli süre, etkinlik için en az 2-3 ay …" | 16 |
| Q23 | [S-035] "Hastalar 3 enjeksiyon siklusu sonra …" | 17 |
| Q24 | [S-035] "6. ÇOCUK VE ERGENDE MİGREN" | 16–18 (ages) |
| Q25 | [S-035] "Hasta fayda görüyorsa enjeksiyonlar 3 ayda bir …" | 16 (excludes) |
| Q26 | [S-035] "Bu tedavide baş ve boyun bölgesinde …" | 18 (type) |
| Q27 | [S-035] "Uygulanım yeri ve dozu …" | 18; 16 (excludes) |
| Q28 | [S-035] "Etkisini değerlendirmek için en az 2 k ez uygulanmalıdır," | 18 |
| Q29 | [S-015] "For full details, see NICE's technology appraisal guidance …" | 01 (excludes) |
| Q30 | [S-106] "The recommended re-treatment schedule is every 12 weeks …" | 01 (excludes) |

**Reformulated invariants that read the tables** (equivalent; checks in section 0):

- **INV-064** (E-046 declarations above):

  ```omn
  ∀ L : ResponderLabel; x : ControlLevel • L.category = controlLevel(x) ⇒
    (∀ p ∈ ran L.evaluated • p.kind ∈ MonthlyKind) ∧ consecutive(L.evaluated) ∧
    (∀ p ∈ ran L.evaluated • courseBegunBy(ctx, L.treatment, p.start)) ∧ evaluatedOnTreatment(L) ∧
    (∀ p ∈ ran L.evaluated; n ∈ levelDays(L, p) • inControlRange(x, n)) ∧
    (∀ mm ∈ controlMinMonths(x) • #L.evaluated ≥ mm) ∧
    (∀ y : ControlLevel; t ∈ forcedAbove(y) • (∀ p ∈ ran L.evaluated • ∃ n ∈ levelDays(L, p) • n > t) ⇒ x = y)
  ```

- **INV-073**:

  ```omn
  ∀ s : AcuteTreatmentSummary •
    (∀ tp : EarlyTimePoint; t ∈ earlyTimePointType(tp) • onlyOfType(ctx, s.typeScope, t) ⇒ s.earlyTimePoint = tp) ∧
    ((¬ ∃ tp : EarlyTimePoint; t ∈ earlyTimePointType(tp) • onlyOfType(ctx, s.typeScope, t)) ⇒ s.earlyTimePoint = twoHours)
  ```

  With SD-ET-01 as the only non-empty case, this is v34's `(onlyOfType(ctx, s.typeScope, c3_1) ⇒ s.earlyTimePoint = fifteenMinutes) ∧ (¬ onlyOfType(…, c3_1) ⇒ s.earlyTimePoint = twoHours)`.

- **INV-085** (after its availability conjuncts move to INV-123):

  ```omn
  ∀ r : ScreeningResult • (∀ s₁, s₂ ∈ r.scores • s₁.subscale = s₂.subscale ⇒ s₁ = s₂) ∧
    ((∃ sb : Subscale • (r.instrument, sb) ∈ dom screeningMax) ⇒
       ∀ s ∈ r.scores • (r.instrument, s.subscale) ∈ dom screeningMax ∧ s.score ≤ screeningMax(r.instrument, s.subscale))
  ```

---

## 7. Facts the context does not state (model section 3.8, rule R-MCF)

### 7.1 Text of the rule (normative, model section 3.8)

> **3.8 Facts the context does not state (R-MCF).** The context may leave a fact unstated:
>
> - the start of a treatment course (`startOf(c, t) = ∅`);
> - the start of the treatment as it was first started (`originalStart(c, t) = ∅`);
> - a course event of a kind (no target or tolerated dose reached, no end of a treatment cycle, no stop or pause);
> - a selection (`previousConsultation`, `chosenPeriod` or `schemeSelection` empty, or fewer than two `comparedSpans`);
> - an instrument or screening result (none available).
>
> One rule applies to every such fact:
>
> 1. **Content aligned to the fact** is asked for only where the context states the fact, and is admitted only where the context states it. Such content is a period placed before or after the fact, a date or duration counted from it, or values compared at a time point counted from it. Its requirement has the antecedent `F ≠ ∅` (or quantifies over `F`), and its tie is `x ∈ F` or `∃ x ∈ F • …` in a definitional or MUST constraint.
> 2. **Content aligned to other facts of the same course** is asked for whether or not the context states the course's start. These facts are a stop, pause or dose reduction, the end of the course, and the as-of date. Where such content is bounded by the start ("on or after the start of the course"), the bound reads "on or after a dated course event of the course" (`courseBegunBy`, E-008). Where the start is stated, this is the same bound, because no course event precedes the start (INV-001). A summary of a period counts an acute course whose start is not stated as started (`courseNotOutside`, E-067).
> 3. **Selections.** Content for a selection is asked for, and admitted, only where the context makes the selection.
> 4. **Results.** A result is shown only where it is available. Content that rests on a result is asked for only where one is available ("Where results … are available", OUT-026, OUT-033).
>
> In the model, "a treatment whose start the context states" replaces "a treatment that has started" (CA-08). Items that apply the rule cite "R-MCF (n)" in their Notes and do not restate it.

### 7.2 The v34 places it replaces, with the verdict in each

None changes. The formal tests in every place are unchanged, except the E-049/INV-070 merge, which is equivalent (`eq_misc.py`). The prose treatments of these places (the "Course start not stated", "Original start not stated" and "Start not stated" paragraphs, and their counterparts in Readings and Conformance fields) are replaced by "R-MCF (n)".

| # | v34 place (formal test) | R-MCF clause | v34 verdict = v35 verdict |
|---|---|---|---|
| 1 | E-041 `inPopulation` (`∃ s ∈ startOf(c, t)`), hence `applicable`, E-043 `timePoints` `when`, INV-055 (second conjunct), INV-058, INV-059 | (1) | no evaluation rule applies, and no time point is asked or admitted, without a stated start |
| 2 | INV-055 first conjunct, INV-102, INV-027, INV-071 (per-phase conjunct), INV-104 (response comparisons): `startOf(c, t) ≠ ∅ ⇒ …` | (1) | asked only where the start is stated |
| 3 | INV-056 `rc.treatmentStart ∈ startOf(…)` (v35: INV-123), INV-068 `∃ s ∈ startOf(…) • …` | (1) | admitted only where the start is stated |
| 4 | E-055 `startDate`, `duration`, `preventiveResponse`, `adherence` (`when startOf(ctx, self.treatment) ≠ ∅`); INV-079 `∀ d ∈ l.duration • startOf(…) ≠ ∅` and its duration ties | (1) | asked, and a duration admitted, only where the start is stated |
| 5 | E-055 `stopDate`, `stopReason` (`when stopped(…)`); INV-079 stop reason (v35: INV-123) | (1), for the stop | asked and admitted only where a stop is stated |
| 6 | E-049 `baseline` (`when originalStart(…) ≠ ∅`); INV-112 `∀ b ∈ v.baseline • ∃ s ∈ originalStart(…) • b.end < s` | (1), for the original start | asked and admitted only where the original start is stated |
| 7 | E-049 `onTreatmentPeriod` `when ∃ s ∈ startOf(…); x … • s < x`, together with the INV-070 conjunct `startOf(…) = ∅ ∧ courseBegunBy(…, plusDays(x, −1)) ⇒ v.onTreatmentPeriod ≠ ∅` | (2) | v35: one `when` clause, the v34 clause verbatim plus a disjunct for unstated starts only (section 8, E-049). The same cases by construction. `eq_misc.py` (970 cases) also shows that both equal the single form `∃ x ∈ firstChangedDay(…) • courseBegunBy(ctx, self.treatment, plusDays(x, −1))`, which v35 does **not** use, because the stated-start case must stay verbatim. Oscillation check 28 allows this merge: watch point 1 ("Not a reversal: moving the ask from INV-070 into the E-049 `when` clause as a disjunct for unstated starts only, provided the stated-start cases stay as they are") and watch point 5 |
| 8 | INV-112 `courseBegunBy(ctx, v.treatment, q.start)`; INV-064 `courseBegunBy(…, p.start)`; INV-067 `courseBegunBy(…, a.window.start)` | (2) | bound by a dated course event |
| 9 | INV-103 (no start condition) | (2) | asked for every stop, pause or reduction |
| 10 | INV-109 `∀ b ∈ startOf(…) • s.period.start = b` and `∀ f … • s.period.start ≤ f.date` | (2) | summary from the start, or from on or before the first dated course event |
| 11 | INV-105 `courseOverlaps` (preventive: a response comparison, aligned to the start) and `courseNotOutside` (acute: a summary of a period) | (1) and (2) | as v34 (fix 16) |
| 12 | INV-078 order of lines by shown start dates | (1) | a line without a start date is not ordered |
| 13 | E-046 `evaluationResult`, `pretreatmentBaseline` (through `rc.treatmentStart`); INV-062 instrument conjuncts | (1), (4) | without a comparison, no score component is decided |
| 14 | INV-094 `∀ d ∈ c.previousConsultation`, `∀ r ∈ c.chosenPeriod`; INV-037, INV-039 `#c.comparedSpans ≥ 2`; E-056 (MAY for contexts with a scheme selection), INV-080 `∃ sel ∈ ctx.schemeSelection` | (3) | asked and admitted only for a selection |
| 15 | INV-081, INV-083, INV-096 (results in range); INV-082, INV-085 availability (v35: INV-123); E-045 `valueAvailable`, INV-062; INV-069 `A ≠ ∅ ⇒ …`; INV-104 results; E-058 `baselineResult` `when` | (4) | as v34 |
| 16 | E-041 `applicable` (`anchorDates(c, t, r.anchor) ≠ ∅`); E-042 `intervalOnTreatment` | (1), for the anchor event | as v34 |

---

## 8. Exact edits to kept items (formal text)

An item not listed here keeps its `omn` block byte-identical. Conjuncts are quoted from v34. "Remove" means: delete the conjunct and the `∧` that joins it.

In this table, `\|` stands for `|`, as in a case-table cell. Inside an `omn` block the author writes a plain `|`.

| Item | Edit |
|---|---|
| E-001 | add `presents` (section 5, INV-119) and `factsShown` (INV-123) to the Definition block |
| E-008 | add `ShownFact`, `inMedicationScope`, `stated` (INV-123) |
| E-009 | label axiom → `axiom table SD-IC` |
| E-010 | `qualifies : set1 →Element  core  shown` |
| E-011 | add `fixedDefinition`, `fixedDefinitionLevel`, `axiom table SD-DF` (INV-125) |
| E-012 | add `daysWithin` (INV-121) |
| E-014 | add `nestedIn` (INV-122) |
| E-028 | `classCode` axiom → `axiom table SD-CLS` |
| E-029 | add `medicationKinds` (section 4.4) |
| E-032 | `axiom (∀ k … ) ∧ overuseCode(combinedUse) = c8_2_6 ∧ basisScope(combinedUse) = ofClasses(classesOf826)` → `axiom ∀ k : AcuteDrugClass • overuseCode(ofClassUse(k)) = classCode(k) ∧ basisScope(ofClassUse(k)) = ofClass(k)`; the `overuseLevel` axiom → `axiom table SD-CLS` and `axiom table SD-CMB`; `const overuseSpanMonths` → SD-FX-06 |
| E-033 | `components : set →PeriodValue  SHOULD when concerns(ctx, self.typeScope, c1)  shown SHOULD when concerns(ctx, self.typeScope, c1)` |
| E-034 | `event : {k : CourseEventKind \| markedKind(k)}  core` (from INV-036) |
| E-035 | `series : →Series  core  shown SHOULD`; `markers : set →TreatmentMarker  SHOULD when …  shown SHOULD` |
| E-038 | `series : →Series  core  shown` |
| E-039 | `series : opt →Series  SHOULD when wholePeriodFrom(self.withdrawalStart, self.covers)  shown SHOULD`; the three `const` lines → SD-FX-03, 04, 05 |
| E-040 | `reference : →DayCount  core  shown MUST when ofResponseComparison(self)`; the same for `compared` |
| E-041 | the rule constants, their axiom and `evaluationRules` → `const evaluationRules : set1 EvaluationRule ≙ table SD-ER` |
| E-042 | `const shortestMonthlyDays` → SD-FX-08 |
| E-043 | `timePoints : … MUST when …  shown MUST` |
| E-045 | the criteria constants, their axiom and `namedCriteria` → `const namedCriteria : set1 ResponderCriterion ≙ table SD-RC` |
| E-046 | `comparison : opt →ResponseComparison  SHOULD  shown SHOULD`; `residual : set →ResidualBurden  SHOULD  shown SHOULD`; `otherValues : set →Item  SHOULD when …  shown SHOULD`; add `inControlRange`, `controlMinMonths`, `forcedAbove` (SD-CL) |
| E-049 | `event : {k : CourseEventKind \| k is stop ∨ k = doseChange(reduction)}  core` (from INV-112); `onTreatmentPeriod : opt →Period  SHOULD when (∃ s ∈ startOf(ctx, self.treatment); x ∈ firstChangedDay(self.event, self.eventDate) • s < x) ∨ (startOf(ctx, self.treatment) = ∅ ∧ ∃ x ∈ firstChangedDay(self.event, self.eventDate) • courseBegunBy(ctx, self.treatment, plusDays(x, −1)))`. The first disjunct is the v34 clause, verbatim. The second is INV-070's antecedent, verbatim, with its `∀ x` turned into `∃ x`; `firstChangedDay` has at most one value, so the two are equivalent |
| E-050 | add `earlyTimePointType` (SD-ET) |
| E-051 | `outcomes : set →OutcomeSummary  SHOULD  shown SHOULD`; `sequence : seq →TreatedAttackLine  SHOULD when self.treatedAttacks > 0  shown SHOULD` |
| E-054 | `preventiveGroups : seq →ClassGroup  SHOULD when …  shown SHOULD`; the same for `acuteGroups` |
| E-055 | `preventiveResponse`, `acuteResponse`, `adherence`: append `shown SHOULD` |
| E-057 | the axioms of `instrumentName` (named instruments), `publishedRecall`, `scoreRange`, `publishedGrading` → `axiom table SD-IN`; `gradeBands` → `const gradeBands : set1 GradeBand ≙ table SD-GB`; delete the domain comments of `publishedRecall` and `scoreRange` |
| E-059 | the three `screeningName` equations → `axiom table SD-SC`; add `fun screeningMax : ScreeningInstrument × Subscale ⇸ ℕ` and `axiom table SD-SR` |
| E-060 | `attacks : set →AttackMark  MUST  shown`; add `shownDayOnes` (INV-124); the two `const` lines → SD-FX-01, 02 |
| E-063 | `const remissionMoreThanMonths` → SD-FX-07 |
| INV-012 | remove `(∀ n : ℕ • coveredDays(n) ∈ ci.expressions ⇒ n ≤ ci.period.lengthDays)` (→ INV-121) |
| INV-024 | keep only the three sum bounds: within the `∀ ks` conjunct, `((∀ k ∈ ks • daysOf(…) ≠ ∅) ⇒ u ≤ Σ …)`, and the two `let` conjuncts. Remove the first two conjuncts and the first two parts of the `∀ ks` conjunct (→ INV-122). New title: "Totals, classes and drugs agree with sums" |
| INV-031 | remove the moderate/severe ≤ headache-days and the symptom-free ≤ headache-free conjuncts (→ INV-122); remove the last conjunct `((∃ mk ∈ v.content ∩ MigraineFreePeriodMark • mk.typeScope = sc) ∧ 0 ∈ daysOf(v, migraineDays, p, sc) ⇒ ∃ mk …)` (CHG-04) |
| INV-032 | remove `(∀ ld ∈ ds • ld.days ≤ i.period.lengthDays) ∧` (→ INV-121) |
| INV-033 | keep only `∀ a : AssociatedSymptomSummary • ∀ n : ℕ; e ∈ viewOf(a).content ∩ AttackCount • a.presence = attacksWithSymptom(n) ∧ sameSpan(e.period, spanOf(a.period)) ∧ e.typeScope = a.typeScope ⇒ n ≤ e.count` (the rest → INV-121, INV-122). New title: "Attacks with an associated symptom do not exceed the attacks" |
| INV-035 | remove `v.series ∈ v.content ∧` and `(∀ mk ∈ v.markers • mk ∈ v.content) ∧` (→ W2) |
| INV-041 | remove `v.series ∈ v.content ∧` (→ W2) |
| INV-050 | in `∀ sr ∈ v.series • sr ∈ v.content ∧ …`, remove `sr ∈ v.content ∧` (→ W2); remove the last conjunct `(plusDays(v.withdrawalStart, 7 × reviewWindowToWeeks) ≤ v.covers.end ⇒ v.reviewWindow ≠ ∅)`, which E-039 `reviewWindow` (SHOULD, no `when`) implies at the same level (CA-05; no change of meaning) |
| INV-056 | remove `rc.treatment ∈ ctx.subject.preventiveTreatments ∧ rc.treatmentStart ∈ startOf(ctx, rc.treatment) ∧` (→ INV-123; CHG-R1) |
| INV-059 | `(∀ tp ∈ rc.timePoints • tp.treatment = rc.treatment ∧ tp ∈ viewOf(rc).content)` → `(∀ tp ∈ rc.timePoints • tp.treatment = rc.treatment)` |
| INV-060 | antecedent: add `∧ ch.compared.period.lengthDays ≥ shortestMonthlyDays` (CHG-03) |
| INV-062 | `(∃ rc ∈ L.comparison • rc ∈ viewOf(L).content ∧ ran L.evaluated ⊆ …` → `(∃ rc ∈ L.comparison • ran L.evaluated ⊆ …`; remove `(∀ x ∈ L.otherValues • x ∈ viewOf(L).content) ∧ (∀ rb ∈ L.residual • rb ∈ viewOf(L).content) ∧` (→ W2) |
| INV-064 | the predicate of section 6 (reads SD-CL) |
| INV-067 | remove `a.treatment ∈ ctx.subject.preventiveTreatments ∧` (→ INV-123) |
| INV-068 | remove `v.treatment ∈ ctx.subject.preventiveTreatments ∧` (→ INV-123; CHG-R1) |
| INV-070 | remove its first conjunct `(∀ x ∈ firstChangedDay(…) • (startOf(…) = ∅ ∧ courseBegunBy(…) ⇒ v.onTreatmentPeriod ≠ ∅))` (→ E-049 `when`) |
| INV-072 | remove `(∀ os ∈ s.outcomes • os ∈ viewOf(s).content) ∧ (∀ l ∈ ran s.sequence • l ∈ viewOf(s).content) ∧` (→ W2) |
| INV-073 | the predicate of section 6 (reads SD-ET) |
| INV-075 | remove its last conjunct (→ INV-123) |
| INV-078 | in `∀ g ∈ … • g ∈ v.content ∧ (∀ l ∈ ran g.lines • l ∈ v.content ∧ …)`, remove `g ∈ v.content ∧` only (→ W2 on E-054); keep `l ∈ v.content` |
| INV-079 | remove the two role conjuncts, `(∀ s ∈ l.startDate • eventOn(…))`, `(∀ e ∈ l.stopDate • ∃ k … eventOn(…))`, `(l.stopReason ≠ ∅ ⇒ stopped(…))`, `(∀ dc ∈ l.doseChanges • eventOn(…))` and the last conjunct (formulations) (→ INV-123). Keep `l.drug = drugOf(l.treatment)`, the duration conjuncts, the three identity ties |
| INV-082 | remove its last two conjuncts (→ INV-123) |
| INV-085 | the predicate of section 6 (reads SD-SR; availability → INV-123) |
| INV-087 | `∀ a ∈ cl.attacks • a ∈ viewOf(cl).content ∧ inSpan(a.onset, cl.cycle)` → `∀ a ∈ cl.attacks • inSpan(a.onset, cl.cycle)` (→ W2) |
| INV-089 | in the `∀ v : ClusterView` conjunct, remove `(∀ b ∈ ran v.bouts; r ∈ ran v.remissions • ∀ bs ∈ b.start; be ∈ lastDay(b); rs ∈ r.start; re ∈ lastDay(r) • be < rs ∨ re < bs)` (→ INV-124) |
| INV-092 | remove `annotated(x, exploratoryMeasure) ∧` (→ INV-120, C3-12) and `(∀ m ∈ x.components • m ∈ viewOf(x).content) ∧` (→ W2); keep `∀ d ∈ x.combines • ∃ m ∈ x.components • dimensionOf(m, d)`. New title: "A migraine composite index shows a component for each dimension it combines" |
| INV-109 | remove `(∀ r ∈ l.preventiveResponse • r ∈ viewOf(l).content) ∧ (∀ s ∈ l.acuteResponse • s ∈ viewOf(l).content) ∧`, and `a ∈ viewOf(l).content ∧` in the last conjunct (→ W2) |
| INV-111 | add a third conjunct (CHG-06): `(∀ v : View; x ∈ v.content; m₁, m₂ ∈ referencedValues(x); lm : LabelledMeasure • isMeasure(m₁, lm) ∧ isMeasure(m₂, lm) ⇒ ∀ l₁ ∈ viewOf(m₁).content ∩ DefinitionLabel; l₂ ∈ viewOf(m₂).content ∩ DefinitionLabel • l₁.measure = lm ∧ l₂.measure = lm ⇒ l₁.definition = l₂.definition)` |
| INV-112 | remove `v.treatment ∈ ctx.subject.preventiveTreatments ∧ (v.event is stop ∨ v.event = doseChange(reduction)) ∧ eventOn(ctx, v.treatment, v.event, v.eventDate) ∧` (→ INV-123 and the E-049 type). New title: "Post-stop monitoring periods are those of the event" |

Realises and Evidence of an edited invariant are unchanged, except that the Realises of every withdrawn or reduced item is carried by the item that takes its content. The checker verifies that the union of Realises per OUT is unchanged (section 14).

---

## 9. Prose policy for the author

### 9.1 Rules per field

**P0 (references and moves).**
- Prose moved to `RATIONALE.md` is moved verbatim, with two exceptions:
  1. References to v34 IDs that are withdrawn in v35 are replaced by their v35 target (section 11, last column), for example "INV-099" → "INV-120 (C3-01)".
  2. A sentence that a CA finding or R35-01 marks as an overclaim is corrected as section 10 states.
- No other wording changes in moved text.
- A paragraph that section 9.2 marks R (dropped) but that contains a sentence quoted in a watch point of oscillation checks 12 to 32, or in a settled point, becomes a D entry instead (check C6, section 14).
- Every source quote (text in double quotes attributed to a source `[S-…]`), with its location, translation and text-layer notes, is preserved verbatim, exactly once, in a `Q` entry (or inside the `N`/`D` entry whose paragraph quotes it).

**Fields:**

| Field | May contain | Moves to `RATIONALE.md` | Dropped (restatement) |
|---|---|---|---|
| Definition / Predicate | the formal text; comments only for units and short glosses (rule U1); no normative comment (CA-11) | — | — |
| Meaning (elements) | (a) one or two sentences on what the element shows, in Stage 1 wording; (b) one gloss per defined predicate or function in the Definition ("`p(x)` holds when …"), as in v34; (c) value-domain remarks the formal text needs (for example `high = ∅` means "no upper bound stated") | sentences giving reasons, sources or Stage 1 justifications → `<ID>/Dnn`; date examples → `<ID>/Wnn` | the audience sentence ("For clinicians and patients.") → catalogue column Audience; sentences stating levels, applicability or other items' content |
| Conformance (elements) | the template: "Availability: <level> (<INV or C1 ID>); applicability: <Stage 1 phrase>, R-MCF (n) where it applies. Definitional: <INV IDs>. Labels and caveats: <C3 IDs>. Prohibited: <C2 IDs>. Placement: <attributes with W2 markers>." Attribute levels are in the declarations and are not repeated | — | every other sentence (the enumerations that restate invariants, CA-08) |
| Reading (invariants) | a paraphrase of the predicate, conjunct by conjunct, naming the defined predicates it uses; nothing that is not a conjunct | "because …", "so that …" → `<ID>/Dnn`; examples → `Wnn` | consequences drawn with other invariants ("Together with INV-…", "This places …"), restatements of other items |
| Notes | (a) "Relations: <IDs>" (IDs only); (b) at most two sentences explaining a formal construct of the item that the Reading or Meaning cannot carry; (c) pointers "See ISS-NN", "R-MCF (n)", "Rationale: <entry IDs>" | everything else, by the per-item table of 9.2: D, N, S, W, X entries | the paraphrase inside "Relations: (…)" and the paragraphs marked R in 9.2 |
| Evidence | "Stage 1 OUT-NNN[ (part)]; [S-NNN] <entry ID>, …" | all quotes → Q entries (Q00 = the lead text of the v34 Evidence field when it contains a source quote; Q01… = its bullets with a quote, in order). A bullet that only points to a quote elsewhere ("[S-001] the subtype labels quoted in E-009") becomes a pointer to that entry | — |

### 9.2 Per-item dispositions of the long Notes (v34 Notes ≥ 900 bytes)

Paragraphs are identified by their first words, as segmented in v34 (bold headings or sentence starts). Codes:
- **K**: keep in the model, shortened to the formal explanation, rule (b) above;
- **D, N, S, W, X**: move to `RATIONALE.md` as the next free entry of that kind under the item (D01, D02, … in the order listed);
- **R**: drop as a restatement;
- **→ ID**: move to the entry of another anchor (used when the content moved to another item).

Items with Notes under 900 bytes follow the default:
- "Relations: (…)" → IDs;
- every "Satisfiab…" sentence → S01;
- every other sentence → D01 (one entry for the rest);
- "See ISS-NN" stays (K).

| Item | Dispositions |
|---|---|
| E-008 | P1 "`PreventiveTreatmentType` lists …": its first five sentences (provenance of the types, examples of listings, `otherPreventive`) K; the rest of P1 ("The guidance type of a treatment is distinct …", "The guidance rules named for all preventive types (E-041) therefore apply …", "A treatment course has at most one start …") R. "**Pause, restart and discontinuation.**" D01. "**Resumed courses.**" D02. "**Course start not stated.**" R (its first two sentences go into model section 3.8, R-MCF (2)). "**Time frames.**" R. Meaning: keep the three time frames as glosses (one line per component) and the predicate glosses; "For a period in which a headache type … correct values" D03; the [S-011] reasoning of the last paragraph D04 |
| E-011 | "`PublishedDefinition` is a given set …" K (first sentence), D01 (the `ihs2025MigraineDay` reason). "**Forms of the measures.**" D02. "**One definition per measure in a view.**" R |
| E-012 | Relations → IDs. "**Type scope of a value.**" D01. "**Time frame.**" R |
| E-013 | Relations paraphrase R. "Stage 1 gives the proportion …" D01. "The 80 % working-group figure …" N01. "OUT-003 asks for the indicator with 'Each reporting period' …" D02. "The treatment history view (E-054) …" R |
| E-018 | Relations paraphrase R. "[S-010] includes moderate-to-severe headache days as a proxy …" D01. "The count is none of the four measures of OUT-002 …" D02; "See ISS-05" K |
| E-023 | Relations → IDs. "The forms are those Stage 1 gives as examples …" D01. "**Periods compared.**" D02 |
| E-029 | Relations paraphrase R. "A day with two classes counts once …" K (one sentence). "The bounds by the sum hold for every period up to the as-of date …" D01. ISS-01 and ISS-09 pointers K |
| E-032 | Relations paraphrase R (CA-04). "The indicators of the same period are those …" K (one sentence on `sameIndicatedPeriod`). "ICHD-3 expresses the levels per month …" D01. "The reading 'on ≥ 10 days/month for > 3 months' …" D02. "Only the medication-use part of ICHD-3 8.2 is shown …" N01. "Because the basis values are shown medication days …" D03. ISS-01 and ISS-09 pointers K |
| E-039 | Relations → IDs. "'The following year' is read as …" D01. "The view begins on the start of withdrawal, and its covered period may end on any day …" D02. "OUT-017 asks for the review window … (ISS-11)" D03 and K pointer. "A subject may withdraw from overused medication more than once …" D04 |
| E-040 | Relations paraphrase R. "The two forms, and the two values compared next to them, are required at MUST only for the changes of a response comparison …" D01. "Such a change may therefore show one form only …" R. "Its two values may be shown in another view …" R |
| E-041 | "**The rule list.**" D01. "**Named, but not evaluation time points**" N01 (with its [S-035] and [S-033] quotes, verbatim). "**Population.**" D02. "**Age on the treatment start.**" D03. "**Types and exclusions.**" D04. "**Readings.**" with its continuation after "(**Stop or pause**, below)" D05. "**Stop or pause.**" D06. Meaning: keep the first sentence, the glosses of `atOffset`, `atLeastOffset`, `withinWindow`, `ageCovered`, `inPopulation`, `applicable` and a one-sentence gloss of `excludes`; the bullet list of time points R (table SD-ER states them); the remaining argument R (D04 holds it) |
| E-042 | Meaning: keep the glosses of `atTimePoint`, `fitsMonthlyPeriod`, `notStoppedBefore`, `intervalOnTreatment`; the two date examples W01, W02. Notes: Relations → IDs; "**Stop or pause.**" (both parts) D01 |
| E-043 | "The baseline and on-treatment periods are calendar months …": "Several consecutive or separate monthly on-treatment periods may be compared with the same baseline month" K; ISS-03 and ISS-10 pointers K; the rest R. "**Stop or pause**" part R |
| E-045 | Meaning: keep one gloss per component kind, `alsoRestsOn`, `PeriodValueKind`, `valueOfKind`, `showsValueNamed`, `conditionHolds`, `valueAvailable`; "`namedCriteria` are the criteria … the '50% responder rate' of [S-002] …" D01; the sentence restating INV-116 R. Notes: Relations → IDs; "NICE 1.3.28 words its measure …" D02; "The second clause of NICE 1.3.29 … is not modelled" N01; "The IHS Q6 MIDAS ranges overlap at a baseline score of 20 …" D03; "The evaluation time point that [S-033] attaches to `critRu71` …" K; "The scheme criteria of OUT-025 …" N02; "Each named criterion is a criterion of its guidance …" D04; "**Named criteria.**" D05; "**Conditions on the treatment.**" D06; "**Other values.**" D07; "**Thresholds on attacks, intensity and duration.**" D08; "**Type scope.**" D09 |
| E-046 | Relations → IDs. Sentences that paraphrase `reductionMet`, `attackReductionMet`, `scoreMet`, `componentDecided` R (the Meaning keeps one gloss each). "For a reduction component, the cited criteria do not state how several months are combined …" D01. "**Type scope**" paragraph ("The periods of these values are matched … by their dates …", the 60 % / 30 % example) D02. "A score component is a criterion of response to the preventive treatment …" D03. "The control-level labels are exactly the four level names … goals for the migraine burden while on treatment …" D04. "**After a stop or pause.**" D05. "Because [S-010] allows insufficient control with fewer than six migraine days …" D06. ISS-08 pointer K |
| E-047 | Relations → IDs. "Stage 1 fixes no measure of adherence …" D01. "**The evaluation window.**" D02 |
| E-049 | Meaning: keep the glosses of the original baseline and `firstChangedDay`. Notes: "'Headache and migraine frequency' is represented by headache days and migraine days; see ISS-03" K; the rest of that paragraph R. "**Resumed treatment.**": the example (1 January … August 2026) W01, "OUT-022 qualifies only the baseline as 'original' …" D01. "**Original start not stated.**" D02 with its example W02. "**Course start not stated.**" D03, verbatim, not R: its sentence "aligned to the event, not to the start" is a watch-point text (check 28, watch point 1; check 32, "E-049 Notes keep …"). Its examples go to W03. The model's E-049 Notes cite "R-MCF (2); Rationale: E-049/D03" |
| E-051 | Relations → IDs. "`outcomes` and `sequence` are references …" R (W2). "Dose changes of acute medications are shown in the treatment history (E-055)" K. "**Formulation of a required summary.**" D01. Conformance (1.9 KB) → template; the enumeration is R |
| E-055 | Relations paraphrase R. "The `when` clauses state when the content can exist …" R (R-MCF (1)). "Every course event lies on or before the as-of date …" D01. "The stop reasons name the failure modes …" D02. "A stop reason states why the course ended …" → INV-123/D03 |
| E-057 | Relations → IDs. "MIDAS grade labels differ between publications …" D01. "The HALT-90 bands of [S-014] overlap at 20 …" D02. "The lower bound 0 …" D03; its last sentence (`high = ∅` meaning) K. "The total scores of MIDAS, PedMIDAS, HALT-90, HALT-30 and HIT-6 are whole numbers …" D04. "HURT grades each response …; see ISS-06" K pointer. "The scoring of every instrument from its answers is out of scope" N01. "`publishedGrading` is fixed by the model only where …" D05. "PGIC in particular exists in several versions (section 11) …" D06 (reference to SL entries). "The value-set functions … are defined only for the tabulated instruments …" R (CA-11, now formal) |
| E-058 | Relations paraphrase R. "A first administration has no earlier result …" K. "The output reports results and their change; it does not make MIDAS or HIT-6 a criterion …" D01. ISS-06 K |
| E-060 | "Relations: INV-087. For every cycle line, in whichever view it is shown …" (the clause-by-clause restatement of INV-087) R. "Reading 'complete cycles the view covers' … is the model's" D01. "A lead-in rests on the summarised diary information …" (to "… every later line shows its day 1") D02. "Only the window of the criterion is shown …" N01. "A prospective diary is not mandatory …" D03. The last sentence (no migraine condition; ISS-03) R with K pointer |
| E-061 | Relations paraphrase R. "An attack in a lead-in is therefore in the window only on days −2 and −1 …" D01. "The mark states nothing about the window of a menstruation whose first day the view does not show …" D02, corrected per R35-01 (section 10). ISS-03 K |
| E-063 | Relations paraphrase R (CA-06). "The output shows the start, end and duration … not the ICHD-3 element … alcohol or nitroglycerine" N01. "`ongoing` is needed so that …" K. "**Time frame.**" D01 (with its example W01). ISS-12 K |
| E-064 | Relations paraphrase R. "The rate is shown with its period …" D01. "Like every count of the model …" D02. "The type scope must be of cluster headache only …" D03 |
| E-067 | "Migraine days are included as OUT-035 states them; see ISS-03" K. "The overview may cover any period …" W01. The rest R |
| INV-001 | Reading: keep the conjunct paraphrase; delete the parenthetical consequences ("so that the guidance time points named for all preventive types apply …"). "The whole-period condition applies to the selected time range only …" D01. "**One stop or pause per course.**" D02. "**Resumed courses.**" D03. "**Time frames.**" R |
| INV-003 | "**Items that refer to the same period atom are in one view.**" K: its first three sentences and the formula; the instance list R. "**Periods of referenced values.**" D01. "Satisfiability: a period atom with given dates …" S01. "**Period atoms with the same dates.**" D02, corrected per CA-12 |
| INV-006 | "A reporting period is identified to the reader by its dates …" D01; "Satisfiable: …" S01 |
| INV-008 | "The antecedent covers every form …" R (E-011/D02 holds it). "The label is an item of the view …" K. "Because the labels of one view for one measure name one definition (INV-111) …" K (one sentence). "Satisfiable in every view …" S01, corrected per CA-07 |
| INV-111 | "A definition label states the definition that its view follows …" D01. "Satisfiability: …" S01, corrected per CA-07 |
| INV-011 | "Every view is a summary output …" D01. "Satisfiable in every view …" S01 |
| INV-031 | "The relations are inequalities …": the sentences on nesting → INV-122/D01; the sentences on `ihs2025MigraineDay` and on migraine days not related to headache days D01 |
| INV-039 | "Where the subject is a child or adolescent …" D01. "**One scale and one form.**" D02. "Satisfiable: …" S01 |
| INV-046 | "The per-class days are read from the class indicators …" D01. "The two directions agree …" S01 (true after CHG-05). "For a subject without acute medication …" S01 |
| INV-049 | "The selected time range consists of whole periods …" D01 with its example W01. "Satisfiability: …" S01 |
| INV-050 | "The start of withdrawal that the view shows is one of the subject's …" R. "The covered period may end on any day … `fillsPeriod` keeps the series tied …" D01. "Satisfiability: …" S01 |
| INV-054 (withdrawn) | "The invariant constrains the changes of response comparisons only …" → E-040/D01 (merge; drop the sentences that duplicate E-040/D01) |
| INV-055 | Reading: keep the conjunct paraphrase, naming `applicable`, `intervalOnTreatment`, `fitsMonthlyPeriod` and `atTimePoint`; the parenthetical paraphrase of `excludes` and of the population R. Notes: "A rule applies only within the population …": its first sentence R; "A preventive treatment given only for another headache type …" D01; "The on-treatment periods … cannot be the end of such a period …" D02. "**Stop or pause.**" (both parts) D03. "Satisfiability: …" S01 with its examples W01 |
| INV-056 | "`values` and `changes` are references …" R. "The co-presence of OUT-018 … is thus required at MUST …" D01 |
| INV-062 | Reading: paraphrase only; the long parentheticals that restate `valueAvailable`, `scopeFor` and `summarisesMedication` are replaced by the predicate names. "The response comparison that a label shows as its underlying values is one of the label's treatment …" R. "Without the availability condition, a label under a criterion that rests on such an instrument …" D01. "Satisfiable with E-058 and INV-082 …" S01. "**Type scope**" part D02. "**Acute treatment and instrument results.**" D03, corrected per CA-15. "Satisfiable with INV-003, INV-011 and INV-072 …" S02 |
| INV-114 | "A label classifies the response to its treatment …" D01. "Satisfiability: …" S01 |
| INV-116 | "A label shows its criterion by its name …" D01. "**Named criteria**" part D02. "Satisfiability: …" S01 |
| INV-117 (withdrawn) | "A label classifies the response to a preventive treatment …" → INV-123/D02. "Satisfiability: …" → INV-123/S01, corrected per CA-14 |
| INV-064 | "The level is read from the days of the evaluated months …" D01 (the `courseBegunBy` part R: R-MCF (2)). "Satisfiable: …" S01 |
| INV-067 | "Where the context states the start …" R (R-MCF (2)). "INV-067 bounds only the first day of the window …" D01 |
| INV-068 | "OUT-021 presents the values 'for the same pre-treatment baseline and on-treatment periods' …" D01. "Satisfiable together with INV-069, INV-097 and INV-102 …" S01. "**Start not stated.**" R (R-MCF (1)), its example W01 |
| INV-069 | "**Values that can be compared.**" D01. "Satisfiable: …" S01 |
| INV-070 | the first two paragraphs R (INV-112; the merged `when`). "Satisfiability: …" S01 |
| INV-112 | "The conjuncts state what the view is and what its periods are …" D01 (the "makes nothing more required" sentences stay in D01). "**Original baseline.**" D02. "**Course start not stated.**" R (R-MCF (2)). "Satisfiability: …" S01 |
| INV-072 | "`outcomes` and `sequence` are references …" R (W2). "The outcome measures and the per-attack lines are the effectiveness that the summary reports …" D01. "A summary may have 0 treated attacks …" K. "A summary of one formulation names at most one formulation …" D02 |
| INV-078 | "`preventiveGroups`, `acuteGroups` and `lines` are references …": the W2 sentences R; "OUT-024 asks for 'a chronological list' that shows the treatments …" D01. "**Order.**" D02 |
| INV-079 | "A course has at most one stop or pause …" R. "**Duration and the course.**" D01 with its example W01. "**Formulation.**" → INV-123/D04. "**Stop reason.**" → INV-123/D03 (merged with the E-055 sentence) |
| INV-109 | "**Dose changes.**" D01. "**With the line.**" R (W2), except "A response comparison shown with a line shows its values, changes and time points in the same view (E-043 Notes) …" R as well. "**Type scope.**" D02. "**Period.**" (including the "Course start not stated" part) D03. "**Formulation.**" D04. "**Adherence.**" D05. "Satisfiability: …" S01 |
| INV-082 | "A result reports an available result of its instrument …" → INV-123/D05. "**Grading.**" D01 |
| INV-087 | The explanation of `plusDays(cl.cycle.to, 1 − windowDaysBefore)` as day −2 of the next menstruation K (two sentences). "This holds whether or not the next cycle is shown …" D01, corrected per R35-01. The lead-in argument R (E-060/D02 holds it). "Neither a lead-in, nor a cycle that began before …" K (one sentence). "The relations of the derived attributes … hold in every view …" K (one sentence) |
| INV-088 | "The acute-treatment summaries are those of the selected time range …" D01. "Satisfiability: …" S01 |
| INV-089 | "The rate relation compares output elements only …" D01. "**Time frame.**" D02. "Satisfiability: …" S01 |
| INV-097 | "Satisfiable together with the other constraints …" S01 |
| INV-098 (withdrawn) | "The paediatric outputs of the OUT-036 Caveat are read as …" → INV-120/D01. "Satisfiability: …" → INV-120/S01 |
| INV-100 (withdrawn) | "OUT-038 names its three indicators as examples …" → INV-120/D02 |
| INV-101 (withdrawn) | Notes → INV-119/D01, with the sentence "INV-043, INV-048 and INV-084 state the same prohibition …" rewritten as a reference to C2-08, C2-04, C2-09 |
| INV-104 | "Headache-free days, symptom-free days and the marks …" D01 with ISS-04 K pointer. "Satisfiability: …" S01 |
| INV-105 | "Migraine days are included as OUT-035 names them …" D01 (ISS-03 K). The "Satisfiability: a covered period of at least 28 days …" paragraph is split: the series and `fillsPeriod` reasoning D02; "The intensity summaries of the time course share the scale …" D03; "A period need not contain the first day of a menstruation …" to "'Where relevant' is read for the covered period …" D04, corrected per CA-16 and R35-01; "The effect of a preventive treatment is shown by a response comparison …" to the end D05; the satisfiability sentences S01. "Satisfiability of the treatment-effect conjunct …" S02 |
| INV-106, INV-107, INV-108, INV-016, INV-017 (withdrawn) | Notes → INV-119/D02 (INV-106: the MUST NOT level), INV-119/D03 (INV-107), INV-118/D01 (INV-108, INV-016, INV-017: the levels of OUT-001 against OUT-006 and OUT-007; section 3.4) |

### 9.3 Other sections

- **Section 4.1 (layers).** Keep v34 section 4's five layers, one or two sentences each, with corrected layer 3 (CA-19): "Per-period values (E-012 … E-031, E-033, E-051, E-064) and the medication-overuse indicator (E-032, an item for one period and one class or combined use, not a `PeriodValue`)". The relation diagram stays.
- **Section 7 (traceability).** Columns: Requirement | Strength (Stage 1, by part) | Catalogue rows | Elements | Invariants | Coverage. Coverage is "full" plus one line per statement part or Caveat: "<part> (<level>): <item IDs, C/SD rows>". The v34 coverage reasons are dropped (restatements; CA-01, CA-04 and CA-06 recur there). Where a reason argues a reading of Stage 1 that no item's rationale holds, move it to `OUT-NNN/D01`. Of the v34 rows, only OUT-018 contains such an argument ("The time points are all those …"), and E-041/D01 already holds it, so none is expected.
- **Section 8 (issues).** Keep the fields Stage 1, Effect on the model, For the human, with these changes:
  - The "Evidence" quotes move to `ISS-NN/Qnn` entries (PROCESS.md section 6, from v35), and the field becomes "Evidence: [S-001] ISS-12/Q01 …".
  - "Effect on the model" keeps its statements, with v35 IDs; the paraphrases of model items are reduced to IDs.
  - ISS-12 Effect is qualified per CA-06 ("a remission period that shows its start date …").
  - ISS-13 is new (section 10, CA-01).
- **Section 9 (withdrawn and merged).** Columns: ID | Name | Iteration | Reason | Went into. The 38 merged invariants of section 11 below, reason "restructuring (PROCESS.md section 6a), merged", plus the v34 ISS-07 row.
- **Section 11 (search log)** → `RATIONALE.md` section 3, verbatim: SL-001 = the first paragraph (search date and tools), then one entry per later paragraph or table, in order.
- **Section 12 (change log).** For v00 to v34, keep each version's first bullet line ("- vNN (iteration NN, date): …") and drop its sub-bullets: the detail stays in `history/vNN.md` and `fixes/fix-iter-NN.md`. The v35 entry is three or four lines, pointing to `fixes/fix-iter-35.md` and this plan.

---

## 10. Disposition of R35-01 and CA-01 to CA-19

`fixes/fix-iter-35.md` handles each of these as a remark: fixed, or kept with justification.

### R35-01 (formal defect: cycle lines outside the menstrual-relation view may overlap)

**Resolution: fixed (CHG-01), by INV-124's first conjunct.** The conjunct is output-wide (the review's option (a), not (b)), and its quantifier covers both kinds of shown first day of menstruation:

`∀ cl, cl₂ : CycleLine • ∀ d ∈ shownDayOnes(cl₂) • ¬ (cl.cycle.from < d ∧ d ≤ cl.cycle.to)`

**Why output-wide.** The review's case 2 (a menstrual-relation view and an overview of one output that state contradictory cycles) is excluded only by the output-wide form. Fix 04's ground supports it: all views of one output summarise the same diary information as of one as-of date.

**Why `shownDayOnes`, and not only `firstDayOfMenstruation`.** E-060 states that a line that has ended shows the first day of the next menstruation, the day after its last day. The architect's random enumeration (`r3501.py` and the refined test):
- v34: 77,875 of 202,196 admitted single-view outputs mark an attack wrongly against a menstruation the view shows; 49,126 of them only on lines that have not ended.
- With the conjunct as the review proposes it: 8,211 of 131,124 still do, 2,529 of them on ended lines. An example is two lead-ins of one view with different ends: the shorter one, having ended, shows a next first day inside the longer one.
- With `shownDayOnes`: 1,816 of 122,410 single-view and 1,149 of 132,625 two-view outputs, all on lines that have not ended.

**What the prose may claim** (INV-087 Reading, D entries of E-060, E-061, INV-087 and INV-105, rows OUT-030 and OUT-035):
> In every view, an attack mark shows the attack as in the perimenstrual window exactly when its onset lies in the window of a menstruation whose first day the view shows (as the day 1 of a line, or as the day after a line that has ended). The exception is an attack on a line that has not ended: its mark states nothing about a menstruation that begins after the line's last day.

This exception is the one v34 already states in E-061 Notes. The claims "every attack mark is correct" and "every window day of a menstruation that the view shows is distinguished" are qualified accordingly.

**Watch points** (oscillation check 12, item 4, carried by check 32, item 5). None of the reversal triggers is hit:
- the lead-in conjunct of INV-087 is unchanged;
- no view or line is required for a period without menstruation;
- the start of the view is unchanged;
- the sequence structure stays in the menstrual-relation view.

**Section 6a: the broader rule.** "The dated phases that one output shows describe one history." It applies equally to the cluster periods and remission periods of E-063, whose non-overlap v34 states only inside one cluster view (INV-089). INV-124 states it for both kinds (CHG-02), and it is the class rule that future remarks on phases are fixed against.

**Stage 1 basis:**
- OUT-030 (MUST): "distinguishing the perimenstrual window as defined in ICHD-3 appendix A1.1 [S-001] from other days of the cycle";
- OUT-035: "where relevant, the relationship to menstruation";
- OUT-031: "using the ICHD-3 definitions". A remission period is attack-free and a cluster period has attacks, so the two cannot overlap.

### CA findings

| ID | v35 resolution | Change of meaning | Intended reading and reason |
|---|---|---|---|
| CA-01 (INV-060 vs INV-061 for compared periods shorter than a month) | INV-060's antecedent gains `ch.compared.period.lengthDays ≥ shortestMonthlyDays`. New **ISS-13** (text below). The E-040 Conformance template and row OUT-019 claim no more than that | **CHG-03** | Fix 02, item 14, settled the reading, and reviews 19c to 35 kept it: "A residual 'per month' … within a shorter compared period does not exist by the wording of Stage 1 itself". v34 kept INV-060 unmeetable for such changes, which excluded from full conformance every percentage change in migraine or headache days over a period shorter than 28 days. Stage 1 forbids no such change (OUT-009 asks for weekly values). v35 keeps fix 02's reading, asks for the residual burden only where one per month exists, and puts OUT-019's "Wherever" for shorter periods to the human |
| CA-02 (INV-031's last conjunct makes the MAY marks more required) | the conjunct is removed. The mark-implies-0 conjunct stays definitional. INV-104 keeps the marks of the clinician-facing summary at SHOULD | **CHG-04** | Section 3.3, item 5: a definitional invariant cannot make an element more required. Marking every 0-migraine-day period once any is marked is content of OUT-008 (MAY), and no Stage 1 SHOULD or MUST part asks for it. At MAY it imposes nothing |
| CA-03 (INV-046's single-class guarantee fails with class indicators for classes never used) | INV-123: a shown acute-medication day count above 0 implies that the subject has used medication of its scope (`usedScope`). INV-046 is unchanged, and its guarantees now hold | **CHG-05** | The prose of INV-046 states ICHD-3's own rule ([S-001] 8.2.3 comment, quoted in INV-046: cumulative use within the class of non-opioid analgesics is not 8.2.6). E-008 holds every acute medication used up to the as-of date, so a positive count of days for a scope never used is a false shown fact (class F7). Acute-treatment summaries are not tied (fix 17's declined tie, check 24, watch point 6) |
| CA-04 (E-032 Notes and row OUT-016 summarise INV-046 incompletely) | E-032's Relations paraphrase and the OUT-016 coverage reason are dropped (prose policy) | no | the predicate governs |
| CA-05 (`reviewWindow` SHOULD in every view vs INV-050's conditional) | the formal reading is kept. INV-050's conditional conjunct is removed as implied by E-039 `reviewWindow` (SHOULD, no `when`). The prose (E-039/D02, INV-049/D01, INV-050/D01) says: the review window SHOULD be shown in every follow-up view, and INV-051 fixes its dates, which may lie after the covered period and the as-of date | no | Fix 02, item 14 ("E-039 `reviewWindow` (SHOULD unconditionally) and the conditional conjunct of INV-050 are consistent") is a settled point (check 32: "E-039 `reviewWindow` without a `when` clause"), with Stage 1 support (OUT-017: "including the review window 4 to 8 weeks after the start of withdrawal"). The audit's alternative, a `when` clause, would narrow a SHOULD and reverse a settled point |
| CA-06 (remission bound only where the start is shown) | prose only. INV-089 Reading, the E-062 and E-063 entries, row OUT-031 and the ISS-12 Effect say "a remission period that shows its start date lasts more than three months; every fully conformant output shows it (E-063 `start`, SHOULD)" | no | Fix 02, item 14 relates E-063's attributes only where they are shown, and check 32 (watch point 1) lists re-tying E-063 as oscillation |
| CA-07 (INV-008 not satisfiable when a change refers to values under two definitions) | INV-111 gains a third conjunct: the values that one change, residual burden or composite index refers to come from views that, where they state a definition for the measure, state the same one. INV-008/S01 and INV-111/S01 then hold as written | **CHG-06** | E-011 ("relations … compare values of one measure under one definition"); OUT-002 Rationale ("different definitions give different numbers"). A change between values under two definitions is not a change of one measure. Fix 32 treated the cross-view case as tied at the level of OUT-002 and did not see that INV-008 is then unmeetable. Not the per-value definitions that check 24 (watch point 2) protects against |
| CA-08 (E-043/E-051 "for each preventive treatment"; "has started") | R-MCF (1) and its wording rule: "a treatment whose start the context states". Conformance fields use the template | no | the predicates govern (INV-055, INV-056, INV-071, INV-102, E-048 since v28) |
| CA-09 (cluster-view references not placed, but described as shown) | prose only. INV-088 Reading says "refers to" for bouts, remissions and rates. No W2 marker on E-062, and INV-011's fourth conjunct is unchanged (it applies where phase items are in the view's content) | no | Fix 11 declined the placement ("OUT-031 lists what to report … without asking for one view"), and review 24 kept it. No new evidence shows fix 11 wrong; the audit's ground is the prose. Section 15 offers the human the alternative |
| CA-10 (E-019 says every attack count is the ICHD-3 frequency of attacks; INV-010 is SHOULD) | prose: E-019 Meaning worded as E-016 and E-017 ("under the one published definition that the view follows for attacks, which its labels name; INV-125, SD-DF-02, asks that the label name ICHD-3 'frequency of attacks' at SHOULD") | no | Stage 1 OUT-007 puts the definition at SHOULD |
| CA-11 (comments have no formal force, yet carry domains and the conditions of `Rep`/`ctx`) | the domains are stated by case tables (SD-IN: `publishedRecall`, `scoreRange`) or by section 2.3's new wording. The `Ctx`/`Rep`/`ctx`/`parts` conditions become normative sentences in section 3.2. Comments keep no formal force | no | the intended reading is normative content stated outside comments |
| CA-12 (INV-003 Notes: "the values that one view shows for periods with the same dates agree") | the paragraph moves to INV-003/D02, limited to INV-006, INV-012, INV-046, INV-089 and INV-122 | no | the predicates govern |
| CA-13 (series–covers tie: definitional for the three-month view, SHOULD for the time-course view) | kept. The difference is stated in INV-041/D01 and is visible in the W2 markers (E-038 `series` `shown`; E-035 `series` `shown SHOULD`) | no | OUT-028 (MUST) defines the view as the three periods (structure). The time-course tie is OUT-009 content at SHOULD. Reviews 31 and 32 kept INV-035 at SHOULD, and re-tying it as definitional is oscillation (check 32, watch point 1) |
| CA-14 (INV-117 Notes: a control-level label can refer to any preventive treatment) | prose: INV-123/S01 says "a responder or non-responder label can refer to any preventive treatment of the subject; a control-level label only to one that has a whole monthly period on treatment (INV-064)" | no | INV-064 governs |
| CA-15 (INV-062 Notes: "None of these values decides a category") | prose: INV-062/D03 says "no acute-treatment summary, and no result of an instrument without a score component (for example PGIC), decides a category; the results at the evaluation and at the pre-treatment baseline decide score components (INV-063)" | no | INV-063 governs |
| CA-16 (INV-105 Reading: the required cycle line is a lead-in) | prose: the Reading says what the conjunct says ("a cycle line that overlaps that period"). The lead-in remark goes to INV-105/D04 as a way to meet the conjunct | no | the predicate governs |
| CA-17 (ℙ T used as a result type, which section 2.4 excludes) | section 2.4 widened (plan section 3.4) | no | the declaration is intended |
| CA-18 (the week convention "of the output") | "of the diary" | no | one given function means one convention |
| CA-19 (section 4 lists the overuse indicator among the PeriodValues) | section 4.1 corrected (plan section 9.3) | no | E-032 governs |

**ISS-13 (new, model section 8).**

> ### ISS-13 Residual burden next to a percentage change over a period shorter than a month
> - Stage 1: OUT-019 asks: "Wherever the output shows a relative (percentage) change in migraine or headache days, it SHOULD show next to it the absolute number of migraine days and moderate/severe headache days per month that remain on treatment." OUT-009 asks for weekly values where weekly granularity is clinically relevant, and the model admits a change between any two periods (E-040).
> - Evidence: Stage 1 wording only. No calendar month or 28-day period lies within a compared period of fewer than 28 days, so a number "per month" within it does not exist (fix 02, item 14).
> - Effect on the model: the residual burden is asked for next to every percentage change in migraine or headache days whose compared period has at least 28 days (INV-060 with INV-061). It is not asked for next to a change over a shorter compared period, for example between two calendar weeks.
> - For the human: decide whether OUT-019 applies to percentage changes over periods shorter than a month, and if so, which month the residual burden then refers to (for example the calendar month or 28-day period that ends on the last day of the compared period).

---

## 11. Mapping of every v34 element and invariant to its v35 place

Generated by `mapping.py` from the parsed v34 items (`items.json`). The table is complete: 67 elements, 117 invariants.

**Counts:**
- 67 elements kept with their IDs; none withdrawn.
- Of the 117 invariants:
  - 50 kept with byte-identical `omn` blocks;
  - 29 kept with the edits of section 8;
  - 38 withdrawn as merged (model section 9: one row each, giving the v35 place).
- v35 therefore has 79 kept v34 invariants plus INV-118 to INV-125, which is 87.

**How to read the "v35 place" column.** It is the target for reference updates (P0, section 9.1). Every reference in v35 to a withdrawn invariant (in Realises, Evidence, Relations, Notes, the traceability table, ISS entries and the RATIONALE entries) is replaced by its v35 place, as follows:
- a C-row, written as "INV-118 (C1-01)";
- a W2 marker, written as "E-040 `reference` (W2)";
- the kept invariant, if a part stays there.

A reference to a kept invariant that lost a conjunct names the item that now holds the conjunct, wherever the sentence is about that conjunct. Example: "INV-031 bounds moderate/severe headache days by headache days" becomes "INV-122".

| v34 ID | v34 title | v35 place | Disposition |
|---|---|---|---|
| E-001 | Element | E-001 | kept; Definition + `presents` (INV-119), `factsShown` (INV-123) |
| E-002 | Output | E-002 | kept; formal text unchanged |
| E-003 | View | E-003 | kept; formal text unchanged |
| E-004 | Item and OtherItem | E-004 | kept; formal text unchanged |
| E-005 | Period | E-005 | kept; formal text unchanged |
| E-006 | Series | E-006 | kept; formal text unchanged |
| E-007 | OutputContext | E-007 | kept; formal text unchanged |
| E-008 | SubjectProfile | E-008 | kept; Definition + `ShownFact`, `inMedicationScope`, `stated` (INV-123) |
| E-009 | ICHD-3 code references | E-009 | kept; label axiom → SD-IC-01…15 (`axiom table SD-IC`); hierarchy axioms stay |
| E-010 | Annotation | E-010 | kept; `qualifies` gets marker `shown` (W2, ex INV-007) |
| E-011 | DefinitionLabel | E-011 | kept; + `fixedDefinition`, `fixedDefinitionLevel`, `axiom table SD-DF` (INV-125) |
| E-012 | PeriodValue | E-012 | kept; + `daysWithin` (INV-121); catalogue OC-35 for the `ofType` scopes |
| E-013 | CompletenessIndicator | E-013 | kept; formal text unchanged |
| E-014 | DayCount | E-014 | kept; + `nestedIn` (INV-122) |
| E-015 | HeadacheDays | E-015 | kept; formal text unchanged |
| E-016 | MigraineDays | E-016 | kept; formal text unchanged |
| E-017 | ModerateSevereHeadacheDays | E-017 | kept; formal text unchanged |
| E-018 | MigraineOrModerateSevereHeadacheDays | E-018 | kept; formal text unchanged |
| E-019 | EventCount and AttackCount | E-019 | kept; formal text unchanged |
| E-020 | HeadacheFreeDays | E-020 | kept; formal text unchanged |
| E-021 | SymptomFreeDays | E-021 | kept; formal text unchanged |
| E-022 | MigraineFreePeriodMark | E-022 | kept; formal text unchanged |
| E-023 | IntensitySummary | E-023 | kept; formal text unchanged |
| E-024 | DurationSummary | E-024 | kept; formal text unchanged |
| E-025 | AssociatedSymptomSummary | E-025 | kept; formal text unchanged |
| E-026 | MostBothersomeSymptomItem | E-026 | kept; formal text unchanged |
| E-027 | Aura measures | E-027 | kept; formal text unchanged |
| E-028 | AcuteDrugClass | E-028 | kept; `classCode` axiom → SD-CLS (`axiom table SD-CLS`) |
| E-029 | AcuteMedicationDays | E-029 | kept; + `medicationKinds` (C1-10, C1-13) |
| E-030 | FunctionalImpactDays | E-030 | kept; formal text unchanged |
| E-031 | CaregiverImpact | E-031 | kept; formal text unchanged |
| E-032 | MedicationOveruseIndicator | E-032 | kept; overuse axioms → SD-CLS, SD-CMB (general rule for `ofClassUse` stays); `overuseSpanMonths` → SD-FX-06 |
| E-033 | CompositeIndex | E-033 | kept; `components` gets marker `shown SHOULD when concerns(…, c1)` (W2, ex INV-092) |
| E-034 | TreatmentMarker | E-034 | kept; `event` typed `{k : CourseEventKind \| markedKind(k)}` (ex INV-036) |
| E-035 | TimeCourseView | E-035 | kept; `series`, `markers` get marker `shown SHOULD` (W2, ex INV-035) |
| E-036 | WeeklyMedicationView | E-036 | kept unchanged; catalogue kind of OC-16 (availability now C1-11) |
| E-037 | PeriodComparison | E-037 | kept; formal text unchanged |
| E-038 | ThreeMonthPatternView | E-038 | kept; `series` gets marker `shown` (W2, ex INV-041) |
| E-039 | WithdrawalFollowUpView | E-039 | kept; `series` gets marker `shown SHOULD` (W2, ex INV-050); three `const` → SD-FX-03, 04, 05 |
| E-040 | Change | E-040 | kept; `reference`, `compared` get marker `shown MUST when ofResponseComparison(self)` (W2, ex INV-054) |
| E-041 | EvaluationRule | E-041 | kept; rule constants, axiom and `evaluationRules` → SD-ER-01…18 (`≙ table SD-ER`) |
| E-042 | EvaluationTimePoint | E-042 | kept; `shortestMonthlyDays` → SD-FX-08 |
| E-043 | ResponseComparison | E-043 | kept; `timePoints` gets marker `shown MUST` (W2, ex INV-059) |
| E-044 | ResidualBurden | E-044 | kept; formal text unchanged |
| E-045 | ResponderCriterion | E-045 | kept; criteria constants, axiom and `namedCriteria` → SD-RC-01…06 (`≙ table SD-RC`) |
| E-046 | ResponderLabel | E-046 | kept; `comparison`, `residual`, `otherValues` get marker `shown SHOULD` (W2, ex INV-062); + `inControlRange`, `controlMinMonths`, `forcedAbove` (SD-CL) |
| E-047 | AdherenceSummary | E-047 | kept; formal text unchanged |
| E-048 | TreatmentReviewView | E-048 | kept; formal text unchanged |
| E-049 | PostStopMonitoringView | E-049 | kept; `event` typed (ex INV-112); `onTreatmentPeriod` `when` gains INV-070's ask as a disjunct for unstated starts (R-MCF (2); equivalent; check 28, watch point 1) |
| E-050 | AcuteOutcomeMeasure | E-050 | kept; + `earlyTimePointType` (SD-ET) |
| E-051 | AcuteTreatmentSummary | E-051 | kept; `outcomes`, `sequence` get marker `shown SHOULD` (W2, ex INV-072) |
| E-052 | OutcomeSummary | E-052 | kept; formal text unchanged |
| E-053 | TreatedAttackLine | E-053 | kept; formal text unchanged |
| E-054 | TreatmentHistoryView and ClassGroup | E-054 | kept; `preventiveGroups`, `acuteGroups` get marker `shown SHOULD` (W2, ex INV-078) |
| E-055 | TreatmentLine | E-055 | kept; `preventiveResponse`, `acuteResponse`, `adherence` get marker `shown SHOULD` (W2, ex INV-109) |
| E-056 | SchemeWindowView | E-056 | kept; formal text unchanged |
| E-057 | Instrument value sets | E-057 | kept; value-set axioms → SD-IN-01…09, `gradeBands` → SD-GB-01…16 |
| E-058 | InstrumentResult | E-058 | kept; formal text unchanged |
| E-059 | ScreeningResult | E-059 | kept; `screeningName` axiom → SD-SC-01…03; + `screeningMax` with SD-SR-01…04 |
| E-060 | MenstrualRelationView and CycleLine | E-060 | kept; `attacks` gets marker `shown` (W2, ex INV-087); + `shownDayOnes` (INV-124); two `const` → SD-FX-01, 02 |
| E-061 | AttackMark | E-061 | kept; formal text unchanged |
| E-062 | ClusterView | E-062 | kept; formal text unchanged |
| E-063 | ClusterPeriodItem and RemissionPeriodItem | E-063 | kept; `remissionMoreThanMonths` → SD-FX-07 |
| E-064 | ClusterAttackRate | E-064 | kept; formal text unchanged |
| E-065 | TriggerCooccurrenceView | E-065 | kept; formal text unchanged |
| E-066 | ClinicianSummary | E-066 | kept; formal text unchanged |
| E-067 | PatientOverview | E-067 | kept; formal text unchanged |
| INV-001 | Admissible contexts | INV-001 | kept; formal text unchanged |
| INV-002 | Period length and kind agree with the dates | INV-002 | kept; formal text unchanged |
| INV-003 | Every view states its period, and every period it uses is shown in it | INV-003 | kept; formal text unchanged |
| INV-004 | A series consists of consecutive periods of its granularity | INV-004 | kept; formal text unchanged |
| INV-005 | A number of days does not exceed the period length | INV-121 | withdrawn as merged (model section 9) |
| INV-006 | One value per measure, period and scope in a view | INV-006 | kept; formal text unchanged |
| INV-007 | An annotation is shown with what it qualifies | W2: E-010 `qualifies` | withdrawn as merged (model section 9) |
| INV-008 | Definition labels for the defined measures | INV-008 | kept; formal text unchanged |
| INV-009 | Headache days follow ICHD-3 | INV-125 (SD-DF-01) | withdrawn as merged (model section 9) |
| INV-010 | Attacks follow ICHD-3 | INV-125 (SD-DF-02) | withdrawn as merged (model section 9) |
| INV-111 | One definition per measure in a view | INV-111 | kept, edited: third conjunct added (CHG-06) |
| INV-011 | A completeness indicator accompanies each reporting period | INV-011 | kept; formal text unchanged |
| INV-012 | Completeness values agree with the period | INV-012 | kept, edited: covered days ≤ length → INV-121 |
| INV-013 | No completeness cut-off presented as clinically validated | INV-119 (C2-02) | withdrawn as merged (model section 9) |
| INV-014 | Headache days per reporting period | INV-118 (C1-01) | withdrawn as merged (model section 9) |
| INV-015 | Migraine days per reporting period, for patients with migraine | INV-118 (C1-02) | withdrawn as merged (model section 9) |
| INV-016 | Moderate/severe headache days per reporting period | INV-118 (C1-03) | withdrawn as merged (model section 9) |
| INV-017 | Attacks per reporting period | INV-118 (C1-05) | withdrawn as merged (model section 9) |
| INV-108 | Moderate/severe headache days and attacks per calendar month or 28-day period, where provided | INV-118 (C1-04, C1-06) | withdrawn as merged (model section 9) |
| INV-018 | Intensity summary per reporting period | INV-118 (C1-07) | withdrawn as merged (model section 9) |
| INV-019 | Duration summary per reporting period | INV-118 (C1-08) | withdrawn as merged (model section 9) |
| INV-020 | Durations of treated attacks are labelled as influenced by acute treatment | INV-120 (C3-03) | withdrawn as merged (model section 9) |
| INV-021 | Durations of treated attacks are not a stand-alone efficacy measure | INV-119 (C2-03; CHG-07) | withdrawn as merged (model section 9) |
| INV-022 | Associated symptoms and most bothersome symptom across periods, for migraine | INV-118 (C1-09) | withdrawn as merged (model section 9) |
| INV-023 | Acute-medication days per reporting period: total, by class and by drug | INV-118 (C1-10) | withdrawn as merged (model section 9) |
| INV-024 | Totals, classes and drugs agree | INV-024 | kept, edited: four ≤ bounds → INV-122; keeps the three sum bounds |
| INV-025 | Weekly view of acute-medication days | INV-118 (C1-11) | withdrawn as merged (model section 9) |
| INV-026 | Functional impact per reporting period | INV-118 (C1-12) | withdrawn as merged (model section 9) |
| INV-027 | Functional impact compared with the baseline period | INV-027 | kept; formal text unchanged |
| INV-028 | Separate presentation per headache type | INV-118 (C1-13) | withdrawn as merged (model section 9) |
| INV-029 | Intensity per headache type, where provided | INV-118 (C1-14) | withdrawn as merged (model section 9) |
| INV-030 | Values per headache type do not exceed the combined values | INV-122 | withdrawn as merged (model section 9) |
| INV-031 | Relations between day measures | INV-031 | kept, edited: two nesting bounds → INV-122; last conjunct removed (CHG-04) |
| INV-032 | Intensity values lie on their scale | INV-032 | kept, edited: level days ≤ length → INV-121 |
| INV-033 | Further bounds of per-period values | INV-033 | kept, edited: pain time, symptom days, caregiver days → INV-121; functional-impact bounds → INV-122; keeps attacks-with-symptom bound |
| INV-034 | Time-course view available | INV-034 | kept; formal text unchanged |
| INV-035 | Time-course content and treatment markers | INV-035 | kept, edited: two placements → W2 (E-035) |
| INV-036 | Markers show the treatment course | INV-123 + E-034 attribute type | withdrawn as merged (model section 9) |
| INV-037 | Comparison of selected periods of equal length | INV-037 | kept; formal text unchanged |
| INV-038 | Comparison values refer to the compared periods | INV-038 | kept; formal text unchanged |
| INV-039 | Intensity can be compared between periods | INV-039 | kept; formal text unchanged |
| INV-040 | Three-month pattern view available | INV-040 | kept; formal text unchanged |
| INV-041 | Structure of the three-month pattern view | INV-041 | kept, edited: `v.series ∈ v.content` → W2 (E-038) |
| INV-042 | Three-month view shows the definitions it refers to | INV-042 | kept; formal text unchanged |
| INV-043 | Three-month view assigns no diagnosis | INV-119 (C2-08) | withdrawn as merged (model section 9) |
| INV-044 | Medication-overuse indicator per period, per class and for combined use | INV-044 | kept; formal text unchanged |
| INV-045 | Medication-overuse indicator agrees with its code, level, span and basis | INV-045 | kept; formal text unchanged |
| INV-046 | Combined use of ICHD-3 8.2.6 | INV-046 | kept; formal text unchanged |
| INV-047 | Indicator worded as a prompt for clinical review | INV-120 (C3-04) | withdrawn as merged (model section 9) |
| INV-048 | Indicator is not a diagnosis of medication-overuse headache | INV-119 (C2-04) | withdrawn as merged (model section 9) |
| INV-049 | Withdrawal follow-up view available | INV-049 | kept; formal text unchanged |
| INV-050 | Withdrawal follow-up content | INV-050 | kept, edited: `sr ∈ v.content` → W2 (E-039); review-window conjunct removed as implied (CA-05, no change) |
| INV-113 | A withdrawal follow-up view shows a start of withdrawal of the subject | INV-123 | withdrawn as merged (model section 9) |
| INV-051 | The NICE CG150 1.3.48 review window | INV-051 | kept; formal text unchanged |
| INV-052 | Label of the expected transient worsening | INV-120 (C3-06) | withdrawn as merged (model section 9) |
| INV-053 | Absolute and percentage change agree with the values they compare | INV-053 | kept; formal text unchanged |
| INV-054 | A change of a response comparison is shown with the values it compares | W2: E-040 `reference`, `compared` | withdrawn as merged (model section 9) |
| INV-055 | Response comparison for each preventive treatment, at the evaluation time points | INV-055 | kept; formal text unchanged |
| INV-056 | Response comparison content | INV-056 | kept, edited: treatment and start facts → INV-123 (CHG-R1) |
| INV-057 | Moderate/severe headache days in the comparison, where reported | INV-057 | kept; formal text unchanged |
| INV-058 | Evaluation time points agree with their rule and anchor | INV-058 | kept; formal text unchanged |
| INV-059 | Evaluation time points shown with the comparison | INV-059 | kept, edited: `tp ∈ viewOf(rc).content` → W2 (E-043) |
| INV-060 | Residual burden next to a percentage change | INV-060 | kept, edited: antecedent restricted to compared periods ≥ 28 days (CHG-03) |
| INV-061 | Residual burden refers to a monthly on-treatment period | INV-061 | kept; formal text unchanged |
| INV-062 | A responder label shows its criterion and the values it rests on | INV-062 | kept, edited: three placements → W2 (E-046) |
| INV-114 | A responder label's response comparison is one of the label's treatment | INV-114 | kept; formal text unchanged |
| INV-116 | A criterion shown under the name of a named criterion is that criterion | INV-116 | kept; formal text unchanged |
| INV-117 | A responder label concerns one of the subject's preventive treatments | INV-123 | withdrawn as merged (model section 9) |
| INV-063 | A responder label agrees with the decidable components of its criterion | INV-063 | kept; formal text unchanged |
| INV-064 | Control levels of the IHS position statement 2025 | INV-064 | kept, edited: reformulated with SD-CL (equivalent) |
| INV-065 | A responder label is not the sole indicator of individual benefit | INV-119 (C2-06; CHG-07) | withdrawn as merged (model section 9) |
| INV-066 | Adherence next to the response comparison | INV-066 | kept; formal text unchanged |
| INV-067 | Adherence refers to the time on treatment | INV-067 | kept, edited: treatment fact → INV-123 |
| INV-068 | Treatment review view: frequency and medication for the same periods | INV-068 | kept, edited: treatment fact → INV-123 (CHG-R1) |
| INV-069 | Treatment review view: further dimensions where provided | INV-069 | kept; formal text unchanged |
| INV-070 | Post-stop monitoring content | INV-070 | kept, edited: presence ask → E-049 `when` (equivalent) |
| INV-112 | Post-stop monitoring shows the subject's event and its periods | INV-112 | kept, edited: treatment and event facts → INV-123, event kinds → E-049 type; keeps the period bounds |
| INV-071 | Acute-treatment summaries per drug, per formulation and per preventive phase | INV-071 | kept; formal text unchanged |
| INV-072 | Acute-treatment summary content | INV-072 | kept, edited: two placements → W2 (E-051) |
| INV-073 | Early time point: 15 minutes for cluster headache, otherwise 2 hours | INV-073 | kept, edited: reformulated with SD-ET (equivalent) |
| INV-074 | Outcome counts agree with the summary and its attack lines | INV-074 | kept; formal text unchanged |
| INV-075 | Attack lines are consistent | INV-075 | kept, edited: medication fact → INV-123 |
| INV-076 | Associated symptoms in the response of treated attacks, for migraine | INV-076 | kept; formal text unchanged |
| INV-077 | Treatment history lists every treatment | INV-077 | kept; formal text unchanged |
| INV-078 | Treatment history is chronological and grouped by drug class | INV-078 | kept, edited: group placement → W2 (E-054); keeps line placement |
| INV-079 | Treatment lines agree with the treatment course | INV-079 | kept, edited: course facts and formulation fact → INV-123; keeps drug, durations, identity ties |
| INV-109 | A treatment line shows every dose change, and its response summary and adherence with it | INV-109 | kept, edited: three placements → W2 (E-055) |
| INV-080 | Scheme windows are the selected windows | INV-080 | kept; formal text unchanged |
| INV-081 | Results of validated instruments where available | INV-081 | kept; formal text unchanged |
| INV-082 | Instrument results agree with the instrument's published value set | INV-082 | kept, edited: availability → INV-123 |
| INV-083 | Screening results next to the headache outputs | INV-083 | kept; formal text unchanged |
| INV-084 | Screening results are not psychiatric diagnoses | INV-119 (C2-09) | withdrawn as merged (model section 9) |
| INV-085 | Screening scores lie in the instrument's range | INV-085 | kept, edited: availability → INV-123; ranges reformulated with SD-SR (equivalent) |
| INV-086 | Menstrual-relation view for patients who menstruate | INV-086 | kept; formal text unchanged |
| INV-087 | Menstrual cycles, the perimenstrual window and attacks | INV-087 | kept, edited: attack placement → W2 (E-060) |
| INV-088 | Cluster-headache view | INV-088 | kept; formal text unchanged |
| INV-089 | Cluster periods, remissions and rates are consistent | INV-089 | kept, edited: bout–remission non-overlap → INV-124 (output-wide) |
| INV-090 | Caveats of the trigger co-occurrence view | INV-120 (C3-09) | withdrawn as merged (model section 9) |
| INV-110 | The dates of a trigger co-occurrence view lie in the period it covers | INV-110 | kept; formal text unchanged |
| INV-091 | No composite index as a primary measure for migraine | INV-091 | kept; formal text unchanged |
| INV-092 | A migraine composite index is exploratory and shown with its components | INV-092 | kept, edited: annotation → INV-120 (C3-12); placement → W2 (E-033); keeps dimension coverage |
| INV-115 | The components of a composite index for migraine are of its period and type scope | INV-115 | kept; formal text unchanged |
| INV-093 | AUC as a primary measure for tension-type headache is shown with headache days | INV-093 | kept; formal text unchanged |
| INV-094 | Clinician-facing summary available | INV-094 | kept; formal text unchanged |
| INV-095 | Patient-facing overview available | INV-095 | kept; formal text unchanged |
| INV-096 | Paediatric outputs: PedMIDAS, school days and caregiver impact | INV-096 | kept; formal text unchanged |
| INV-097 | Paediatric comparisons use periods of equal length | INV-097 | kept; formal text unchanged |
| INV-098 | Paediatric outputs are presented as supportive information | INV-120 (C3-11) | withdrawn as merged (model section 9) |
| INV-099 | Interpretive caveats on every summary | INV-120 (C3-01) | withdrawn as merged (model section 9) |
| INV-100 | Indicators, labels and associations require clinical interpretation | INV-120 (C3-05, C3-07, C3-08, C3-09, C3-10) | withdrawn as merged (model section 9) |
| INV-101 | No output presented as replacing clinical assessment or as a diagnosis | INV-119 (C2-01) | withdrawn as merged (model section 9) |
| INV-102 | Treatment review view available for each preventive treatment | INV-102 | kept; formal text unchanged |
| INV-103 | Post-stop monitoring available after a stop, pause or reduction | INV-103 | kept; formal text unchanged |
| INV-104 | Clinician-facing summary content | INV-104 | kept; formal text unchanged |
| INV-105 | Patient-facing overview content | INV-105 | kept; formal text unchanged |
| INV-106 | No output decides on the continuation of a preventive treatment | INV-119 (C2-05) | withdrawn as merged (model section 9) |
| INV-107 | No output decides which definition of acute treatment response applies | INV-119 (C2-07) | withdrawn as merged (model section 9) |

---

## 12. Intended changes of meaning

Every other difference between v34 and v35 is a move, with the equivalence argued in sections 5 to 8 and checked by the scripts named in the header.

"Narrows" or "widens" refers to:
- the admitted outputs (definitional constraints);
- the MUST-conformant repertoire;
- the fully conformant repertoire (section 3 of the model).

| ID | Items | Formal change | Effect on admitted sets | Reason | Stage 1 basis |
|---|---|---|---|---|---|
| **CHG-01** | INV-124 (1st conjunct); E-060 `shownDayOnes` | A cycle line of any view does not span a first day of menstruation that the same output shows: no line's day 1, and no day after an ended line, lies after the first day and on or before the last day of another line | Narrows the admitted outputs: outputs whose cycle lines contradict one another, or contradict the day 1s of the menstrual-relation view. Every context keeps an admitted output: lines drawn from one sequence of menstruations meet it (INV-087 already orders the lines of one view this way). | R35-01: an attack mark is correct only against the menstruations the view shows. v34 bounds this only inside the menstrual-relation view. Random test: in v34, 77,875 of 202,196 single-view outputs had a wrong mark; with the conjunct, 1,816 of 122,410 had one, all on lines that have not ended (section 10) | OUT-030 (MUST, ICHD-3 A1.1 window), OUT-035; fix 04 (all views of one output summarise one diary as of one date) |
| **CHG-02** | INV-124 (2nd and 3rd conjuncts); INV-089 (the bout–remission conjunct removed as implied) | Output-wide, for items whose start and last day are shown: two cluster periods are the same period or do not overlap; two remission periods likewise; a cluster period and a remission period do not overlap | Narrows the admitted outputs: outputs whose cluster or remission periods contradict one another across views, or inside a view outside the consecutive pairs that INV-089 orders | The class rule of R35-01 (PROCESS.md section 6a), applied to the other dated phases of the model | OUT-031 ("using the ICHD-3 definitions" [S-001] 3.1.1, 3.1.2: a remission period is attack-free, a cluster period has attacks) |
| **CHG-03** | INV-060 (antecedent); ISS-13 | The residual burden is asked for only next to a percentage change whose compared period has at least `shortestMonthlyDays` (28) days | Widens the fully conformant repertoire. In v34 no output with a percentage change in migraine or headache days over a period shorter than 28 days was fully conformant, because INV-060 asked for what INV-061 forbids. The MUST level is unchanged | CA-01: an unmeetable SHOULD. The reading of fix 02, item 14 ("per month" within a shorter period does not exist) is kept, and the open question goes to the human (ISS-13) | OUT-019 ("per month"), OUT-009 (weekly values), OUT-018 |
| **CHG-04** | INV-031 (last conjunct removed) | A view that marks one period without migraine days is no longer required to mark every period of the view with 0 migraine days for the type scope. The conjunct "a mark implies a count of 0" stays | Widens the admitted outputs at every level, by views that mark some but not all such periods. In the clinician-facing summary, INV-104 (SHOULD) still asks for the marks of the covered period and of each series period | CA-02: a definitional invariant cannot make an element more required (section 3.3, item 5, the rule on which fixes 30 and 31 were decided) | OUT-008 (MAY: "periods without migraine days"); OUT-034 via INV-104 |
| **CHG-05** | INV-123 (`usedScope` member of `factsShown`) | A shown acute-medication day count above 0 for a scope (all acute medication, a class, a set of classes, a drug) implies that the context lists an acute medication of that scope | Narrows the admitted outputs, by outputs that state a positive count of medication days for medication the subject never used. A count of 0 stays admitted (fix 17's reason for declining the summary-formulation tie) | CA-03: without it, INV-046's guarantee (one class alone does not reach ICHD-3 8.2.6) fails for class indicators of classes never used | OUT-014; E-008 (every acute medication used up to the as-of date); [S-001] 8.2 comments quoted in INV-046 |
| **CHG-06** | INV-111 (3rd conjunct) | The values that one change, residual burden or composite index refers to come from views that, where both state a definition for the measure, state the same one | Narrows the admitted outputs and the MUST-conformant repertoire, by outputs that themselves state two definitions for the two values of one change. The fully conformant repertoire is unchanged: none of these outputs could meet INV-008 (CA-07, `inv111.py` of the audit) | CA-07; E-011 (relations compare values of one measure under one definition) | OUT-002 and its Rationale ("different definitions give different numbers") |
| **CHG-07** | INV-119 for C2-03 (v34 INV-021) and C2-06 (v34 INV-065) | A prohibited claim carried by an annotation that qualifies the element counts as presenting the element with that claim, as v34 already reads for INV-048 and INV-084 | Narrows the fully conformant repertoire (SHOULD NOT level only): `eq_g2g3.py` found 349 differences in 100,000 models, all of this kind | One reading of "presented as" for every prohibited claim. v34's difference between C2 rows has no Stage 1 basis | OUT-011 Caveat ("should therefore not present duration of treated attacks as a stand-alone efficacy measure"); OUT-020 ("SHOULD NOT be presented as the sole indicator of individual benefit") |
| **CHG-R1** | INV-056, INV-068 (the treatment and start facts) → INV-123 | The level of these conjuncts goes from MUST to definitional. Their content is unchanged | **No change of meaning.** No output whose context lacks these facts meets MUST, so the MUST-conformant and fully conformant repertoires are the same. Only the label of the violation changes ("not an output" instead of "not MUST-conformant"). It is listed because a reader of levels sees a change | Fix 32's class rule: a false shown fact is excluded definitionally (check 32, watch point 1: moving a tie *up* is not a reversal) | — |

**No other change of meaning.** In particular:
- Every value, code, threshold, set and quote is unchanged (sections 6 and 9.1).
- Every level is unchanged except CHG-R1.
- No `when` clause is narrowed or widened. E-049's clause gains INV-070's ask without change (section 7.2, row 7).
- No element is withdrawn.
- No Stage 1 statement part loses its realising item (section 14, check C3).

---

## 13. Watch points and how v35 keeps each decision

Sources: the "Things the next checker should watch" lists of checks 12, 16, 24, 28 and 32; fix 02, item 14; fix 11; fix 17; reviews 31 and 32. "Verbatim" means character-identical formal text, wherever v35 puts it.

| Watch point (source) | Protected decision | v35 | Checker verifies |
|---|---|---|---|
| Identity ties, "truth of a shown fact" (check 32, wp 1) | INV-112 to INV-117; INV-079's v30 and v32 conjuncts; INV-082/085 availability; fix 32's attribute table; the ties earlier fixes declined | Every tie becomes a verbatim member of `factsShown`/`stated` in INV-123, at definitional level (CHG-R1 moves two up, none down). INV-113 and INV-117 are withdrawn as merged, not dropped. INV-112, 114, 115 and 116 are kept. Fix 30's duration conjunct and fix 28's `∀ d ∈ l.duration • startOf(…) ≠ ∅` stay in INV-079, verbatim. No declined tie is added: not fix 18's evaluated periods, fix 17's summary formulation, E-063 or E-058 (CA-06 is prose only), INV-078 grouping, INV-035 at definitional (CA-13), or adherence windows bounded by the stop. `E-046.comparison` stays `opt`, and the W2 marker relies on it. CHG-05 adds one member to the class (CA-03, not a review remark) | INV-123's equivalence (section 5) for each replaced conjunct. Every protected term of check 32's `guar.py` list is present in v35's formal text. Future members are rows of `factsShown`, judged against INV-123/D01 (fix 32's table, updated) |
| Named criteria (check 32, wp 2; check 12, wp 2; check 16, wp 4) | INV-116; forced "non-responder" (`set1`); open list of criteria (R08b-01); `K = n` not taken | INV-116 unchanged. `const namedCriteria : set1 ResponderCriterion ≙ table SD-RC`: the case table defines the constant, not the type, so `ResponderCriterion` stays open. INV-063 unchanged. INV-064 is reformulated with SD-CL, equivalent | SD-RC cells against the v34 terms (script). `eq_misc.py`'s INV-064 method (29,520 cases) |
| Comparability (check 32, wp 3) | `onSameScale`, `inSameForm`; INV-027, 039, 069, 105; INV-018, INV-029 and INV-062 not tied | INV-027, 039, 069 and 105 byte-identical. INV-018 and INV-029 become cells C1-07 and C1-14: availability only, no tie added | Byte-identity; the C1 cells |
| Treatment-course cluster (check 32, wp 4; check 28, wps 1–5) | INV-070 presence ask at SHOULD; `courseBegunBy`, `originalStart`, `resumes`; E-049 `when` clauses; INV-112 bounds; start-tied bounds of fix 28; one stop per course | The presence ask moves into E-049's `when` as a disjunct for unstated starts only. The stated-start clause is verbatim and the level is SHOULD; check 28, wp 1 names exactly this move "not a reversal", and wp 5 allows the merge. The INV-070 baseline and `shownDay` conjunct, INV-112's period bounds, INV-001 and the `courseBegunBy` bounds of INV-064, 067, 068, 078, 079 and 109 are verbatim. Only their fact conjuncts move to INV-123, and their placements to W2. E-049's sentence "aligned to the event, not to the start" moves verbatim to E-049/D03 (section 9.2). The three fix-28 sentences that fix 29 corrected are not restored: moved prose is v34's | Section 8, rows E-049, INV-070, INV-112. A stop on the start day asks for the on-treatment period and a reduction on the start day does not (check 24, wp 4): the first disjunct is v34's |
| By-dates relations (check 24, wp 1) | `daysOf` by dates; INV-006 identity; the INV-031 marks conjunct by `sameSpan`; output-wide agreement of counts is a new decision | INV-122 quantifies over `daysOf` (by dates) and keeps INV-030's `sameSpan(e.period, spanOf(f.period))` verbatim. INV-006 unchanged. INV-031 keeps "a mark implies 0" verbatim; its completeness conjunct is removed (CHG-04), which is not one of the listed reversals. No agreement of counts across views is added. INV-124 concerns phases only, and its output-wide form is a new decision, taken on fix 04's ground | `eq_misc.py` method (nesting, 100,000 models) |
| INV-111 and INV-008 (check 24, wp 2) | INV-008's predicate; per-value definitions not taken | INV-008 unchanged. INV-111 gains a third conjunct about the two values of one relation (CHG-06), not per-value definitions | Byte-identity of INV-008 |
| Cluster view (check 24, wp 3; fix 11) | `ongoing`/`lastDay`; `e ≤ ctx.asOf`; `remissionMoreThanMonths` and the `plusMonths(s, …) ≤ e` form; `onlyOfType`; the rate relation; the placement fix 11 declined | INV-089 keeps all of these verbatim. The constant moves to SD-FX-07 with the same value and name. The bout–remission conjunct moves to INV-124, output-wide (CHG-02 implies it). There are no W2 markers on cluster-view references (CA-09) | INV-089 diff = the one conjunct (section 8) |
| Day convention and stop bounds (check 24, wp 4) | Section 2.8; `notStoppedBefore`, `intervalOnTreatment`, `evaluatedOnTreatment`; course-event dates | Unchanged | Byte-identity |
| `fillsPeriod` (check 24, wp 5; check 8, wp 4; check 12, wp 5) | 28-day anchor; INV-050 start ties | Unchanged. INV-050 loses only the placement (W2) and the review-window conjunct that E-039 implies (CA-05). The E-039 `reviewWindow` stays without a `when` (check 32) | Section 8, INV-050 |
| Formulation ties (check 24, wp 6; fix 17) | INV-075/079 formulation conjuncts; INV-074; the declined summary-formulation tie | The formulation conjuncts are members of INV-123 at the same level. INV-074 is unchanged. CHG-05 ties day counts above 0 only, not summaries | INV-123's equivalence |
| Text-only entries (check 24, wp 7) | E-057 Notes; ISS-02, ISS-03 and the section 3.5 list; ISS-12 | Moved verbatim (P0). Two additions: ISS-12 Effect gains the CA-06 qualification, and E-057 Notes gain no new text. No earlier wording is restored: the history files (`history/v00.md` … `v34.md`) contain no "shows its start date" | Diff of moved text |
| Earlier watch points (check 24, wp 8; check 16) | INV-105 with E-067; history-wide `acuteMedications`; E-062 `acute`; E-045 `valueAvailable`; acute and adherence identity ties; responder labels; E-041; INV-098; co-presence; menstrual-relation view; withdrawal follow-up; E-008 time frames | INV-105, E-067, E-062, E-008 and `valueAvailable` unchanged. E-041 → SD-ER with cells verbatim. INV-098 → C3-11 (`eq_g2g3.py`: annotations 0 mismatches). Co-presence → INV-118, with v34's `∃ g` placement per measure group (`eq_g1.py` 0 of 200,000; the mutation test shows the placement matters). INV-087's lead-in conjunct is unchanged | The scripts' methods on v35's text |
| Periods beyond the as-of date (check 24, wp 10) | Comparison periods may reach beyond the as-of date | Nothing new bounds them. INV-124 constrains only phases against one another | — |
| Menstrual relation (check 12, wp 4; check 32, wp 5) | INV-087 lead-in; no line for a period without menstruation; the view's start; the sequence stays in the view | All kept (section 10, R35-01) | INV-087 diff = the placement conjunct only |
| Fix 02, item 14 | E-063 and E-058 derived attributes shown independently; no per-month residual within a shorter period | CA-05 and CA-06 are prose only. CA-01 keeps the reading (CHG-03 follows from it, ISS-13) | — |
| Reviews 31 and 32 | INV-035 at SHOULD; INV-078 grouping | W2 markers `shown SHOULD` (E-035) and `shown SHOULD` on E-054's groups only. `ClassGroup.lines` placement stays in INV-078 | W2 table, section 5 |
| Change volume (check 32, wp 6) | Volume falls | v35 touches every item's prose by design. Its formal changes are the 7 CHG entries plus the moves of sections 5 to 8. The next oscillation check should count formal blocks against the section 11 mapping, not raw item counts | Section 14, check C1 |

---

## 14. Risks, checks and size estimate

### 14.1 Risks

| # | Risk | Mitigation |
|---|---|---|
| R1 | Content lost in moves: a conjunct, a quote or a Realises entry. Formal moves touch 38 withdrawn invariants, 29 edited invariants and 30 edited elements; prose moves touch every item | Checks C1–C5 below, by script, before review |
| R2 | A case-table cell differs from the v34 term: a typo in 13 SD tables (94 rows) or in the 35 C rows | The author generates the tables from v34 by script, and the checker parses them back (C4) |
| R3 | The generic invariants are harder to read than the specific ones they replace | The catalogue gives one row per kind of output with its cells. Each C-row names its v34 ID in RATIONALE `C1-NN/D01`. Section 2.11 gives one worked unfolding per form |
| R4 | The reviewer of iteration 36 reads the restructuring as a sweep and raises remarks on moved text | `fixes/fix-iter-35.md` states the CHG list and links this plan. The review checks the CHG list and the equivalence claims, not the moves themselves (PROCESS.md section 6a) |
| R5 | The oscillation check after iteration 36 flags watch-point blocks that changed in form | Section 13 lists each one with its argument. The mapping gives every v34 ID's v35 place |
| R6 | An R paragraph (dropped) holds a sentence that a watch point protects | Rule P0 addition: a paragraph marked R that contains a sentence quoted in a watch point (checks 12–32) or in a settled point becomes a D entry instead. The author greps every quoted watch-point sentence in v35 + RATIONALE.md (C6) |
| R7 | RATIONALE.md drifts from the model | RATIONALE.md section 1: the model governs. Fixes update both, and the review reads RATIONALE only for evidence |
| R8 | The size gain is smaller than expected | Most of the gain comes from Notes and quotes, which move. The model's formal text shrinks by about 10 % only |

### 14.2 Checks (author before handing over; checker repeats)

| # | Check | Pass criterion |
|---|---|---|
| C1 | ID accounting | Every E-001 … E-067 and INV-001 … INV-117 occurs in v35, either as an item or as a section 9 row. The rows and places are those of section 11. New IDs are exactly INV-118 … INV-125, OC-01 … OC-45, C1-01 … C1-14, C2-01 … C2-09, C3-01 … C3-12, SD-…, ISS-13 |
| C2 | Formal identity | The `omn` blocks of the 50 unchanged invariants and 37 unchanged elements are byte-identical to v34. The 29 edited invariants and 30 edited elements differ from v34 exactly by the section 8 edits (a script applies the edits to v34 and compares) |
| C3 | Traceability | For every OUT-NNN, the union of the Realises fields of v35 items, mapped back through section 11, equals the v34 union. Every statement part with a level (MUST, SHOULD, MAY, SHOULD NOT, MUST NOT) has an item or a C/SD row at the same level |
| C4 | Case tables | Each formal cell parses and equals the v34 term (white space aside). The ⇸ domains equal the v34 domains. `default` values match v34's "otherwise" terms |
| C5 | Quotes | The multiset of source-attributed quotes in v34 sections 1–10 (180 occurrences, `sizes.py`), plus section 11, equals the multiset in v35 + RATIONALE.md. Each quote occurs once, in a Q entry or in the D/N entry that holds its paragraph |
| C6 | Watch-point text | Every sentence quoted in a "should watch" list of checks 12 to 32 (for example "aligned to the event, not to the start") is still present, in the model or in RATIONALE.md |
| C7 | Equivalence re-run | Re-run the method of `eq_g1.py`, `eq_g2g3.py`, `eq_misc.py` and `r3501.py` on v35's text: 0 mismatches outside the CHG entries. CHG-07 accounts for the SHOULD NOT differences |
| C8 | Levels | Count invariants per level. v34 levels: MUST, SHOULD, MUST NOT, SHOULD NOT, definitional, repertoire. Minus the withdrawn ones, plus the generic ones (level-indexed counted per C-row), these equal v35's counts, except CHG-R1 (two conjuncts) |
| C9 | Scope | The case tables hold output values that sources fix (codes, labels, thresholds, ranges, rules). None holds input data, a storage format or a derivation from input. Section 2.11 says so |
| C10 | Prose | No Reading states a conjunct that its predicate lacks. No Conformance field says more than its template. CA-04, CA-06, CA-08, CA-10, CA-12, CA-14, CA-15 and CA-16 are corrected as section 10 states |

### 14.3 Size estimate

| File | v34 | v35 estimate | Main contributions |
|---|---|---|---|
| `OUTPUT_MODEL.md` | 822 KB | **400–450 KB** | Sections 1–3: ~45 KB (+ case tables, W2, R-MCF). Section 4: ~45 KB (catalogue and C tables). Section 5: ~145 KB (formal text ~70 KB; Meaning ~35 KB; templates, pointers and short Notes ~40 KB). Section 6: ~115 KB (87 invariants: predicates ~60 KB; Readings ~30 KB; rest ~25 KB). Section 7: ~25 KB. Section 8: ~18 KB. Sections 9 and 10: ~9 KB. Section 11 (SD): ~30 KB. Section 12: ~12 KB (first lines only; v34: 133 KB) |
| `RATIONALE.md` | — | **300–350 KB** | Moved Notes ~170 KB; quotes ~70 KB with their entry headers; reasons from Meaning and Reading ~25 KB; search log ~47 KB; entry overhead ~50 KB; minus dropped restatements ~40 KB |

The two files together come to about 750 KB. The change-log sub-bullets (≈120 KB) leave the model, but stay in `history/` and the fix logs.

The two largest items in v35:
- E-041: formal text plus the SD-ER table, about 15 KB, against 45 KB in v34;
- E-008: about 11 KB, against 21 KB.

---

## 15. Decisions for the human

1. **ISS-13 (CA-01, CHG-03).** Does OUT-019's "wherever" apply to percentage changes over periods shorter than a month, and if so, which month does the residual burden refer to? v35 asks for it only for compared periods of at least 28 days.
2. **Output-wide consistency of dated phases (CHG-01, CHG-02).** v35 takes the review's option (a), output-wide, on fix 04's ground: one output summarises one diary. The alternative is to tie lines only within each view (option (b)), which leaves the review's case 2: two views of one output that state different cycles. Recommended: (a).
3. **The remaining exception of R35-01.** A line that has not ended may still mark an attack wrongly against a menstruation after its last day, as E-061 states. Closing it would require either restricting lead-in lines (a watch-point reversal, check 12, wp 4) or showing the next first day for lines that have not ended (new content, no Stage 1 basis). v35 keeps the exception and states it.
4. **CA-02 (CHG-04).** v35 removes the completeness conjunct of the marks of periods without migraine days. The alternative is to keep it as content, at SHOULD, for every view that marks such periods. This would narrow full conformance beyond INV-104 without a Stage 1 SHOULD. Recommended: remove.
5. **CA-07 (CHG-06) level.** v35 makes the new conjunct definitional, with INV-111. The alternative is SHOULD, which would leave MUST-conformance as in v34. Recommended: definitional (E-011: a change compares values of one measure under one definition).
6. **CA-09 (cluster-view references).** v35 keeps fix 11 (no placement in the view; prose says "refers to"). The alternative is W2 markers `shown SHOULD` on `bouts`, `remissions` and `rates`, which would reverse fix 11 and narrow full conformance.
7. **E-049/INV-070 merge.** It is allowed by check 28 (watch points 1 and 5) and keeps the stated-start clause verbatim. If the human wants v35 to leave every watch-point block untouched, both may stay as in v34, and nothing else depends on the merge.
8. **The class "truth of a shown fact" (CHG-05).** CA-03 adds one more member (positive day counts). With INV-123 the class has one rule and an explicit member list. The human may decide that further members are added by the fixer under PROCESS.md section 6a without a separate decision.
