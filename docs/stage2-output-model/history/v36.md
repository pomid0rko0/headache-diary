# Headache diary — formal model of output data (Stage 2)
Version: v36 · Iteration: 36 · Status: under review
Baseline: Stage 1 OUTPUT_REQUIREMENTS.md v18 (converged)
Companion: RATIONALE.md v36

## 1. Scope and exclusions

This document is a formal, representation-independent model of the information content of the headache diary's outputs: the kinds of output, the elements each output contains, their types, value domains and units, their conformance levels and applicability conditions, the relations between elements, and the invariants every valid output satisfies. It realises the Stage 1 requirements OUT-001 to OUT-039 (baseline v18). "Output" means anything the diary produces for a reader (patients, parents and caregivers, clinicians, researchers and registries).

Out of scope (Stage 2 PROCESS.md section 2), and not described anywhere in this document:

1. **Input data**: what the patient provides to the diary, data fields, data-entry questions, their frequency, reminders and the data-entry interface. The model has no input entities.
2. **Storage format**: persistence, databases, files, serialization or exchange formats, encodings, storage keys, versioning of stored data, retention.
3. **Derivation from input**: any rule, formula, counting procedure, algorithm, decision logic or threshold whose arguments include input data, for example how headache days are obtained from what the patient provided, or how an instrument's total score is obtained from the answers.

In scope, and contained in the model: thresholds, formulas and computed (derived) fields that are part of the output data, that is, values shown to the reader (for example the ICHD-3 reference levels shown with the medication-overuse indicator, a named responder criterion with its threshold, an instrument category shown with its score, the evaluation time points of a response comparison) and relations whose arguments are all output elements (for example a percentage change against the absolute change and the baseline value, or a total across drug classes against the per-class values). Every derived attribute is marked `derived` (section 2.7). Where its value depends only on other output elements, the model states the relation. Where its value is obtained from diary information, the model gives only its type, unit and meaning.

Conditions of applicability ("for patients with migraine", "where results are available") are properties of the output context (section 3.5). They are not decision logic over input data. Technical delivery formats are out of scope.

## 2. Notation

### 2.1 Overview

The model is written in OMN ("output model notation"), a typed first-order set notation defined in this section. OMN takes the mathematical toolkit of Z (sets, tuples, sequences, free types, abbreviations) and the view of Alloy that instances of element types are atoms related by attributes. OMN is a specification notation only. It has no execution semantics, no storage or encoding, and its element types describe output elements shown to a reader, not data structures. Element types and value types are the notation's records with named attributes (Stage 2 PROCESS.md section 3). OMN text appears in fenced blocks marked `omn` and in the formal columns of case tables (section 2.11). Everything else (Meaning, Reading, comments, the informative columns of tables) is explanatory.

### 2.2 Lexical conventions

- **Identifiers** consist of letters, digits, subscript digits (`₁`, `₂`) and `_`. Type names begin with an upper-case letter. Attribute, constant, function, predicate, enumeration-constant and variant-tag names begin with a lower-case letter. Bound variables and parameters may begin with either case (for example `L` for a responder label, `K` for a set of values); a name bound by a quantifier, a comprehension, a parameter list or `let` is a variable in its scope, not a type.
- **Comments** run from `--` to the end of the line. They explain meaning and units and have no formal force.
- **Literals**: numerals (`0`, `15`, `2.5`) denote members of ℕ or ℚ; text literals `"…"` denote members of `Text` and are used for names and labels that an output shows exactly as a source words them.
- **Infix symbols** declared by a function or predicate with underscores (for example `_⊑_`) are written infix (`h ⊑ t`).

### 2.3 Paragraphs

A model is a set of paragraphs. Each name is declared once.

- `given N₁, …, Nₖ` declares **given sets**: non-empty sets whose members have no internal structure in the model. Their meaning is stated in prose.
- `type N == T` declares an **abbreviation**: N denotes the same set as the type expression T.
- `enum N ::= c₁ | … | cₙ` declares an **enumeration**: N is the set of the n pairwise distinct constants c₁, …, cₙ.
- `variant N ::= t₁ | t₂ ⟨T₂⟩ | …` declares a **tagged variant** (free type). A tag without payload is a constant of N. A tag with payload ⟨T⟩ is an injective constructor from T to N. The constants and the ranges of the constructors are pairwise disjoint, and N is their union.
- `value N { a₁ : T₁; …; aₙ : Tₙ } [where φ]` declares a **value type**: N is the set of tuples with named components a₁ … aₙ, restricted to the tuples satisfying φ when a `where` clause is given. Values have no identity; equality is componentwise. `N(a₁ ↦ e₁, …, aₙ ↦ eₙ)` denotes the tuple with the given components.
- `[abstract] element N [extends M] { … }` declares an **element type** (section 2.5).
- `const c₁, …, cₖ : T` declares **given constants**. `const c : T ≙ e` declares a **defined constant**.
- `fun f : T₁ × … × Tₙ → T` declares a **given total function**; `⇸` instead of `→` declares a given partial function whose domain is stated by a case table (section 2.11), by an axiom, or, for the library functions of section 2.8, in that section's list, which defines the library. Where none of these states it, the model constrains the domain only through the invariants that use `dom` (for `classOf`, INV-001). `fun f(x₁ : T₁, …, xₙ : Tₙ) : T ≙ e` declares a **defined function**.
- `pred p(x₁ : T₁, …, xₙ : Tₙ) ≙ φ` declares a **defined predicate**, an abbreviation for the formula φ with the parameters substituted.
- `axiom φ` states a fact about given constants and given functions, for example a table of their values. An axiom contains no free variables and refers to no output element; it fixes the meaning of the constants and functions it mentions.
- `axiom table N` states the axioms of case table N; `const S : set1 T ≙ table N`, `fun f(…) : T ≙ table N [default e]` and `pred p(…) ≙ table N` define S, f or p by case table N. Case tables (section 2.11) give cases of given and defined functions and constants.

### 2.4 Type expressions

- the primitive types of section 2.8, given sets, and the names of enumerations, variants, value types, element types and abbreviations;
- `opt T`: the subsets of T with at most one member (absent = ∅, present = {x});
- `set T`: the finite subsets of T; `set1 T`: the non-empty finite subsets;
- `seq T`: the finite sequences of members of T, that is, functions from 1..n to T for some n ∈ ℕ; `seq1 T`: the non-empty ones;
- `ℙ T`: all subsets of T, finite or not (used for parameters of predicates and functions, for the result types of defined functions and the components of values that hold sets of atoms, for example `fiDays` (E-030) and the catalogue columns (section 4.4), and for the semantic constants of section 3.2);
- `T₁ × T₂`: ordered pairs (x, y); `p.1` and `p.2` are the components;
- `→R`, where R is an element type: references to atoms of R (section 2.5);
- `{c₁, …, cₖ}`: the set of the listed constants of one enumeration or variant, used as a type;
- `{x : T | φ}`: the members of T that satisfy φ. When T is an element type, this is a subset of its atoms.

### 2.5 Element types, atoms, composition and references

- **Atoms.** An instance of the model (an *output structure*) is a set of atoms together with the values of their attributes. Each atom has exactly one most specific, non-abstract element type, and it belongs to that type and to every type that type extends. An element type R used as a term denotes the set of its atoms. An `abstract` type has no atoms except those of its subtypes. Two element types are disjoint unless one extends the other. `extends` is single inheritance; attributes are inherited.
- **Attributes.** Each attribute declaration has the form `a : T [derived] level [when φ] [shown [MUST | SHOULD] [when ψ]]`, with `level` one of `core`, `MUST`, `SHOULD`, `MAY` (section 3.3); the last part is a placement marker (rule W2). Every atom x of the type has a value x.a ∈ T. Different element types may declare attributes with the same name; in `e.a` the attribute is that of the type of e. In `when φ`, `self` denotes the atom and `ctx` the context of the output it belongs to (section 3.2).
- **Typing rule for levels.** An attribute of level `SHOULD` or `MAY`, or of level `MUST` with a `when` clause, has a type of the form `opt T`, `set T` or `seq T`, so that absence is expressible. An attribute of level `core`, or `MUST` without `when`, may have any type.
- **Composition.** An attribute whose type mentions an element type R without `→` holds atoms that are parts of the holder. In this model only `Output.views` and `View.content` are composition attributes. Every `View` atom is part of exactly one `Output` atom, and every `Item` atom is part of exactly one `View` atom. `outputOf(x)` is the output an atom belongs to (an output belongs to itself), and `viewOf(x)` is the view an item is part of; both are given total functions, declared in E-002 and E-003, whose values this composition fixes.
- **References.** An attribute whose type mentions `→R` holds atoms of R. **Rule W1:** every referenced atom belongs to the same output as the holder. References create no parts. `refs(x)` denotes the set of atoms that the attributes of atom x reference directly. Where a referenced atom must be shown in the holder's view, the model states it: for periods, INV-003, which also places in one view every two items that refer to the same period atom (INV-003 Notes), and shows in a view the dates of the periods of the values that a change, a residual burden or a composite index shown in it refers to (`referencedValues`, E-011); for the other references, a placement marker (rule W2) or one of the invariants INV-060, INV-078 and INV-087, which section 6.0 names with the references they place.
- **Rule W2 (placement).** An attribute whose type mentions `→R` may carry a placement marker after its level and `when` clause: `shown` (definitional), `shown MUST` or `shown SHOULD`, optionally followed by its own `when ψ` (with `self` and `ctx` as in the attribute's `when` clause). `shown` is a keyword; a `when` clause ends before it. For every atom x of the type for which ψ holds (every atom, where the marker has no `when`; the attribute's own `when φ` does not restrict the marker), every atom y that x.a references satisfies `∀ h ∈ home(x) • y = h ∨ y ∈ h.content`, where `fun home(x : Element) : set View ≙ {v ∈ {x} ∩ View • v} ∪ {i ∈ {x} ∩ Item • viewOf(i)}` (the view itself for a view, and the item's view for an item). A marker without a level is part of the element's definition (section 3.3, item 5). A marker with a level holds at that level (section 3.3, item 8). Typing rule: a marker only on an attribute whose type mentions `→R`. The attributes that carry markers are listed in section 6.0.

### 2.6 Terms and formulas

Terms:

- variables, constants, literals, `self`, `ctx`;
- `e.a`: the attribute a of an atom e, or the component a of a value e. For an attribute of type `opt T` the term denotes a set with at most one member;
- function application `f(e₁, …, eₙ)`; `dom f`, the domain of a partial function f; tuples `(e₁, e₂)`; value construction `N(a₁ ↦ e₁, …)`;
- a type name used as a term denotes the set it names (for an element type, its atoms); set display `{e₁, …, eₙ}`; comprehensions `{x : T | φ}`, `{x ∈ S | φ}`, `{x ∈ S | φ • e}` (the set of the values of e for the members x of S that satisfy φ) and `{x ∈ S • e}` (the same with φ = true); `S ∪ S′`, `S ∩ S′`, `S \ S′`;
- `#S`: the number of members of a finite set S, or the length of a sequence S;
- for a sequence s: `s(i)` (the i-th member, defined for i ∈ dom s), `dom s` (= 1..#s), `ran s` (the set of members), `first(s)` = s(1) and `last(s)` = s(#s) (defined for non-empty s);
- `i..j`: the set of integers from i to j;
- arithmetic `+`, `−` (binary and unary), `×`, `÷` on ℤ and ℚ (`÷` is defined only for a non-zero divisor and gives a member of ℚ); `Σ x ∈ S • e` (the sum of e over a finite set S, 0 for S = ∅); `max S`, `min S` for a non-empty finite set S of numbers or dates.

Formulas:

- `true`, `false`; `=`, `≠`; `<`, `≤`, `>`, `≥` on numbers, dates and durations; `∈`, `∉`, `⊆`;
- `¬`, `∧`, `∨`, `⇒`, `⇔`;
- `∀ x : T • φ`, `∃ x : T • φ`, `∃₁ x : T • φ`, and the bounded forms `∀ x ∈ S • φ`, `∃ x ∈ S • φ`. Several variables may be declared at once: `∀ x, y : T • φ`, `∀ x, y ∈ S • φ`, or a list of declarations separated by `;` (`∃ x : T; y ∈ S • φ`), in which a later declaration may refer to the variables of earlier ones (`∀ c ∈ Ctx; t ∈ c.subject.preventiveTreatments • φ`);
- `e is t`, for a value e of a variant and a tag t of that variant: `e = t` if t has no payload, `∃ y • e = t(y)` otherwise;
- `x ≈ e` (section 2.7); application of a defined or given predicate;
- `let N == e • φ`: φ with every occurrence of the name N replaced by the term e (a local abbreviation).

Precedence, from strongest to weakest: `¬`, `∧`, `∨`, `⇒`, `⇔`. `⇒` associates to the right. The body of a quantifier extends as far to the right as possible; `•` separates the declaration from the body.

Bound variables take the type of the set they range over. In `∀ x ∈ S ∩ K • φ`, where S and K have different element types, x has the narrower type.

**Definedness.** Partial operations (`÷`, `s(i)`, `first`, `last`, `max`, `min`, partial functions) are used only where the formula guards them, for example `r.days > 0 ⇒ … ÷ r.days`. In `φ ∧ ψ` and `φ ⇒ ψ`, φ guards ψ; a bounded quantifier `∀ x ∈ S` guards its body with `x ∈ S`; and a context or definitional invariant guards the terms whose definedness it ensures in every admissible context and every valid output (for example INV-001 ensures that `classOf(m.drug)` is defined for every acute medication m of a context, INV-002 that `DateSpan(from ↦ p.start, to ↦ p.end)` satisfies its `where` clause, and INV-004 that `periodEndFrom` is defined in `mostRecent`). An unguarded partial term is a type error, not a false formula. An attribute of type `opt T` is used as a single value only inside a quantifier over it (`∀ y ∈ e.a • …`, `∃ y ∈ e.a • …`).

### 2.7 Derived attributes, relations and shown numbers

- An attribute marked `derived` is a computed field of the output data (for example a change from baseline, a total, a proportion, an indicator status, an instrument category). Where all arguments of its relation are output elements, the relation is an invariant of section 6 and is listed under "Relations" in the element's Notes. Where its value is obtained from diary information, the model states only its type, unit and meaning, because the derivation from input is out of scope.
- **Shown numbers.** Numbers shown to the reader may be rounded. `x ≈ e`, where x is a shown number and e an exact rational term, means that x equals e rounded half away from zero to the number of decimal places with which x is shown. Counts of days, attacks and cycles are integers and are shown exactly.
- **Units.** The comment of every numeric attribute states its unit. Rule U1: an output shows the unit together with every numeric value it shows.
- Thresholds, reference levels and offsets taken from sources are written as numerals in constant definitions or in the formal cells of the source data tables (section 11). Each is supported by a verbatim quote in the `RATIONALE.md` entry that the element's Evidence field or the table row names, or by the Stage 1 quote that already contains it (cited by requirement and source ID).

### 2.8 Primitive types and library

The primitive types and the library are declared in this block and explained in the list after it.

```omn
given 𝔹, ℕ, ℕ₁, ℤ, ℚ, Date, Duration, Text
type Percent == {q : ℚ | 0 ≤ q ∧ q ≤ 100}
fun next : Date → Date
fun plusDays : Date × ℤ → Date
fun days : Date × Date ⇸ ℕ₁
fun plusMonths : Date × ℤ → Date
fun isMonthSpan : Date × Date → 𝔹
fun isWeekSpan : Date × Date → 𝔹
fun periodEndFrom : Granularity × Date ⇸ Date
fun minutes : ℚ → Duration
fun hours : ℚ → Duration
fun daysLong : ℕ → Duration
value DateSpan { from : Date; to : Date } where from ≤ to
pred inSpan(d : Date, r : DateSpan) ≙ r.from ≤ d ∧ d ≤ r.to
```

(`given` is used here only to introduce the names of the primitive types; their meaning is the standard one stated below, not an uninterpreted set.)

- `𝔹` = {true, false}.
- `ℕ`: the non-negative integers; `ℕ₁`: the positive integers; `ℤ`: the integers; `ℚ`: the rational numbers; with the usual order and arithmetic, and with ℕ₁ ⊆ ℕ ⊆ ℤ ⊆ ℚ.
- `Percent`: the rationals from 0 to 100. Unit: %.
- `Date`: the days of the Gregorian calendar, totally ordered by `≤` (earlier before later). Library:
  - `fun next : Date → Date`: the following day;
  - `fun plusDays : Date × ℤ → Date`: `plusDays(d, 0) = d`, `plusDays(d, n + 1) = next(plusDays(d, n))`, and negative n count backwards;
  - `fun days : Date × Date ⇸ ℕ₁`: defined for d₁ ≤ d₂; the number of calendar days from d₁ to d₂, both included (`days(d, d) = 1`, `days(d₁, next(d₂)) = days(d₁, d₂) + 1`);
  - `fun plusMonths : Date × ℤ → Date`: the date with the same day of the month n calendar months later (earlier for negative n); if that day does not exist in the target month, the last day of that month;
  - `fun isMonthSpan : Date × Date → 𝔹`: true if and only if the first date is the first day and the second date the last day of the same calendar month;
  - `fun isWeekSpan : Date × Date → 𝔹`: true if and only if the first date is the first day of a calendar week under the week convention of the diary (one convention for all its outputs) and the second date is `plusDays` of the first by 6. Which weekday begins a week is a presentation choice that Stage 1 does not fix;
  - `fun periodEndFrom : Granularity × Date ⇸ Date`: the last day of the period of the given granularity (E-005) that begins on the given date: for `calendarMonth`, the last day of that month (defined when the date is the first day of a month); for `fourWeekPeriod`, `plusDays(d, 27)`; for `calendarWeek`, `plusDays(d, 6)` (defined when the date begins a calendar week).
- `Duration`: non-negative amounts of time, totally ordered, with `+`. `fun minutes : ℚ → Duration`, `fun hours : ℚ → Duration`, `fun daysLong : ℕ → Duration` (whole days), with `minutes(60) = hours(1)` and `hours(24) = daysLong(1)`. A duration is shown with a unit (rule U1).
- `Text`: reader-facing natural-language text in the language of the output. Texts are compared only by equality.
- `DateSpan`: a span of consecutive days, used in contexts and in items that are not reporting periods; `inSpan(d, r)` holds when d lies in r.
- **Day convention.** A date is a whole calendar day, and every period, span and window includes its first and its last day (`days`, `inPeriod`, `inSpan`). The dates of a treatment course and of an evaluation are read as follows wherever the model compares them with a period:
  - **Course events** (E-008). A course includes the day it starts, its first day on treatment. A dose change, and the reaching of the target or tolerated dose, are dated on the first day at the new dose. The end of treatment cycle n (`cycleEnd(n)`) is dated on the first day after that cycle, the day by which the cycle is complete (for a cycle that another follows, the first day of the next). A stop or a pause, of which a course has at most one (INV-001), is dated on the last day of the course, which the course's duration and span include (INV-079, INV-109; `courseOverlaps` and `courseNotOutside`, E-067); the first day off treatment is the day after it (`firstChangedDay`, E-049). A treatment resumed after a stop or pause is a new course, with its own start (E-008).
  - **Intervals and the dates after them.** An interval of n weeks or n months *from* a day a consists of the days from a to `plusDays(a, 7 × n − 1)`, or to the day before `plusMonths(a, n)`. The date *after* the interval (for example "after 12 weeks of treatment", "3 to 6 months after starting", "4 to 8 weeks after the start of withdrawal") is the first day after it, `plusDays(a, 7 × n)` or `plusMonths(a, n)` (`shift`, E-041): the date on which an evaluation or a review falls (E-042, INV-051).
  - **Periods that end with an interval.** A period ends with the interval, and so ends at the date after it, when its last day is the day before that date, `next(p.end) = d` (`atTimePoint`, E-042). A span lasts more than n months from a when its last day is on or after `plusMonths(a, n)` (INV-045, INV-089), and "the following year" from a consists of the days from a to the day before `plusMonths(a, 12)` (INV-049).

### 2.9 Invariants and their scope

Invariants are named predicates (section 6). Each states its scope in its Conformance field:

- **output** (the default): the predicate is evaluated in each output o separately. A quantifier over an element type, `∀ x : R` or `∃ x : R`, ranges over the atoms of R that belong to o, and `ctx` denotes `ctx(o)`;
- **repertoire**: the predicate quantifies explicitly over `Ctx`, `Rep` and outputs (section 3.2). A quantifier over an element type ranges over all atoms; `parts(o)` restricts to one output;
- **context**: the predicate constrains every admissible context; it has the free variable c of type `OutputContext`.

In an output-scope invariant, a quantifier `∀ x : Element` ranges over the atoms of o, so that a table cell that names an element type (for example `View` in table C3) is used only through such a quantifier.

### 2.10 Type checking

The model is well typed when every name used is declared exactly once (or is a primitive of section 2.8 or a semantic constant of section 3.2); every attribute selection `e.a` is applied to a term whose type declares or inherits a; every argument has the parameter's type or a subtype or subset of it (an atom of an element type matches `→R` and `ℙ R` for R itself or a supertype); constants and tags belong to the expected enumeration or variant; the typing rule for levels (section 2.5) holds; and every partial term is guarded (section 2.6).

### 2.11 Case tables

A case table is a table of the model that states axioms or definitions by cases, one row per case. It is a way of writing OMN paragraphs and describes no storage. Its caption, the line directly above it, reads `Case table <ID> — <form>` and names the OMN declarations it gives cases for. Every case table of the model denotes its paragraphs wherever it stands; the paragraph forms below name a table at the place where the functions or constants it gives cases for are declared.

- **Formal and informative columns.** A column whose header is code-formatted (`` `…` ``) is formal. Every other column (for example Row, Source, Rationale) is informative and has no formal force.
- **Cells.** A formal cell holds one OMN term or formula in code format. In a cell, `\|` stands for `|`, and `<br>` is white space. The cell `—` states no case.
- **Form V: constants of a value type.** The caption names a value type T, and may name a collecting constant S. The key column, headed `` `k` ``, lists new constant names, and every other formal header is a component name of T; every component of T has a column. The row with key k and cells e₁ … eₙ denotes `const k : T` and `axiom k = T(a₁ ↦ e₁, …, aₙ ↦ eₙ)`. If the caption names S, the table also denotes `const S : set1 T ≙ {k₁, …, kₘ}`, the set of its keys.
- **Form M: members of a set.** The caption names `const S : set1 T`. Every formal header is a component name of T, and each row denotes the member T(a₁ ↦ e₁, …). The table denotes `const S : set1 T ≙ {the rows' members}`.
- **Form C: cases of functions and predicates.** One or more key columns are headed `` `x₁ : K₁` ``, …. Each key cell is a ground term of its type. Every other formal header is an application `f(x₁, …, p₁, …)` of a function or predicate declared in an `omn` block, with the key variables first and further parameters p declared there; the arguments may be terms built from the key variables (for example `overuseLevel(ofClassUse(k))`).
  - If f is a **given** function (section 2.3), each non-`—` cell e denotes the axiom `f(keys) = e`, or, for a 𝔹-valued f, `f(keys)` for the cell `true` and `¬ f(keys)` for `false`.
  - A given **partial** function (`⇸`) whose cases are given by a case table has as its domain exactly the keys whose cell is not `—`.
  - If f is declared `fun f(x₁ : K₁, …, p : P) : T ≙ table N default e` or `pred f(…) ≙ table N`, the table is f's definition by cases: f(x…, p…) is the cell of the row whose keys are x…, and the default (for a predicate, false) where no row has these keys or the cell is `—`.
- **Form D: defined constants.** The formal columns are headed `` `k` ``, `` `type` `` and `` `value` ``. The row with cells k, T and e denotes `const k : T ≙ e`.
- **Paragraph forms.** `axiom table N` states the axioms of case table N. `const S : set1 T ≙ table N`, `fun f(…) : T ≙ table N default e` and `pred p(…) ≙ table N` refer to a case table as the definition.
- **Type checking.** The keys of a table are pairwise distinct. Every cell is well typed (section 2.10) with the key variables and parameters in scope.
- **Worked unfoldings** of each form are in `RATIONALE.md`, entry SEC-2.11/W01.
- **Scope.** The case tables of section 11 hold values that a source fixes and that the output shows or relates (codes, labels, reference levels, ranges, bands, evaluation rules, criteria); the case tables of section 4.4 hold the cases of the generic invariants. No case table holds input data, a storage format or a derivation from input (section 1).

## 3. Conformance

### 3.1 Levels

The levels are those of RFC 2119 as clarified by RFC 8174, in upper case: MUST, MUST NOT (absolute requirement or prohibition), SHOULD, SHOULD NOT (recommended or not recommended; a deviation is acceptable only for a valid reason in particular circumstances, understood and weighed), MAY (truly optional). In addition, `core` marks an attribute that is part of an element's identity, and "definitional" marks an invariant that is part of an element's definition (section 3.3).

The levels are also values, used by the level-indexed invariants (section 3.3, item 7) and by the catalogue and source data tables:

```omn
enum Level ::= must | should | may | shouldNot | mustNot
```

### 3.2 Conformance target and semantic constants

The conformance target is the diary's **repertoire**: the set of outputs it can produce, each paired with the context it is produced for.

```omn
const Ctx : ℙ OutputContext                     -- the admissible output contexts
const Rep : ℙ (OutputContext × Output)          -- the repertoire
fun ctx : Output → OutputContext                -- the context of an output
fun parts : Output → set Element                -- the parts of an output
pred provides(K : ℙ Element) ≙ ∃ p ∈ Rep • ∃ x ∈ parts(p.2) • x ∈ K   -- the diary provides content of kind K somewhere in its repertoire
```

`Output` is the element type of E-002, and `OutputContext` the value type of E-007. `Ctx` is the set of `OutputContext` values that satisfy the context invariants (INV-001). `Rep ⊆ Ctx × Output`: (c, o) ∈ Rep when the diary produces output o for context c. For every output o, (ctx(o), o) ∈ Rep, and no output is paired with two contexts. `parts(o)` = {o} ∪ o.views ∪ {i | v ∈ o.views ∧ i ∈ v.content}.

A diary is **MUST-conformant** when its repertoire satisfies every definitional invariant (section 3.3) and every MUST and MUST NOT constraint of this model. It is **fully conformant** when it also satisfies every SHOULD and SHOULD NOT constraint, except where a valid reason in particular circumstances justifies a deviation (RFC 2119); the model does not formalise such reasons. MAY constraints impose nothing: they state that the content is permitted and fix its type and meaning.

### 3.3 How levels attach

1. **Availability of an element kind.** The Conformance field of an element states whether the diary MUST, SHOULD or MAY be able to produce it, and under which applicability condition. Each such statement is formalised by a repertoire invariant named in that field. "K is available when C" means: for every context c ∈ Ctx that satisfies C, some output o with (c, o) ∈ Rep contains an atom of K with the stated content. For per-period measures, the repertoire invariant is INV-118 with its catalogue cases (table C1).
2. **Attributes.** For an attribute `a : T level when φ` of type `opt T`, `set T` or `seq T`, the presence constraint "for every atom x of the type for which φ holds, x.a is not empty" holds at the given level. An attribute of level `MUST` without `when`, or of level `core`, is present by typing. `core` marks an attribute that is part of the element's identity: an atom without it would not be an instance of the element. A `core` attribute carries no level of its own; it is present whenever the element is. `MAY` imposes no presence constraint.
3. **Element and attribute levels.** An attribute's level applies to every atom of the element that exists. An element whose availability is SHOULD or MAY has MUST attributes only where a MUST statement part of Stage 1 requires that content in every such element; the attribute then cites that part (for example the reporting period of OUT-001, which every summary output MUST state).
4. **Invariants.** Each invariant has one level, except a level-indexed invariant (item 7), which has one level per instance. An invariant of level MUST NOT or SHOULD NOT has a predicate of the form `¬ F`; F is the prohibited situation, and the invariant is satisfied when F does not occur.
5. **Definitional invariants.** An invariant that states the relation of a derived attribute to other output elements, a bound that follows from an element's definition (for example a number of days within a period), or the structure of an element (for example that a series is consecutive) is *definitional*. It is part of the meaning of the element: an atom that does not satisfy it is not an instance of the element. A definitional invariant has no level of its own. It holds wherever the element is shown, and the level of the element or attribute decides whether the element is shown at all. It therefore cannot make an element more or less required; it excludes only outputs that show a value contradicting the definition of the element, which no Stage 1 requirement permits. Definitional invariants are marked "definitional" in their Conformance field, with the elements whose definition they are part of (for INV-001, the set `Ctx` that it characterises).
6. **Stage 1 strength.** Every level follows the strength of the Stage 1 statement part that the element, attribute or invariant realises (Stage 2 PROCESS.md section 4). A prohibition that is the negative form of a Stage 1 statement part or caveat (for example "supports but does not replace clinical assessment and diagnosis", or "reports scores as screening results, not as psychiatric diagnoses") has the negative level of the same strength: SHOULD NOT for a SHOULD part, MUST NOT for a MUST part. A constraint is stronger than one part only where another part of at least that strength directly requires it, and it then cites both parts. Purely structural primitives take the level of the requirement that needs them.
7. **Level-indexed invariants.** An invariant whose Conformance field reads "level-indexed" has a predicate Φ with one free variable l of type `Level`. For each l ∈ {must, should, shouldNot, mustNot}, the instance Φ[l] is a constraint at level MUST, SHOULD, SHOULD NOT or MUST NOT. The instance Φ[may] imposes nothing. An instance at SHOULD NOT or MUST NOT has the form ¬ F (item 4). The level of every case that an instance reads from a table follows the Stage 1 strength of the statement part named in that row (item 6).
8. **Placement markers.** A placement marker `shown L` (rule W2, section 2.5) holds at level L for every atom of the type for which its `when` clause holds. `shown` without a level is definitional (item 5).

### 3.4 Repertoire predicates used by availability invariants

```omn
pred reportedPerPeriod(c : OutputContext, K : ℙ PeriodValue, sc : TypeScope) ≙
  ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views • ∃ sr ∈ v.content ∩ Series •
    tiles(sr, c.timeRange, c.granularity) ∧ perPeriod(v, sr, K, sc)
```

`reportedTogether(c, Ks, sc)` is the same for several kinds at once, in one view and one series:

```omn
pred reportedTogether(c : OutputContext, Ks : ℙ (ℙ PeriodValue), sc : TypeScope) ≙
  ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views • ∃ sr ∈ v.content ∩ Series •
    tiles(sr, c.timeRange, c.granularity) ∧ ∀ K ∈ Ks • perPeriod(v, sr, K, sc)
```

`reportedPerPeriod(c, K, sc)` holds when some output produced for c contains a view with a series of consecutive periods that spans the selected time range at the selected granularity, and shows, for every period of that series, a value of kind K with type scope sc (E-006, E-012). Where Stage 1 says "per reporting period" without naming a granularity, the availability invariant requires `reportedPerPeriod` for contexts of at least one granularity; where Stage 1 names calendar months or 28-day periods (OUT-001), at least one of these two.

OUT-001's frequency outputs are read as the frequency measures of OUT-004 to OUT-007 (OUT-009 wording); see ISS-04. Their availability per calendar month or 28-day period is stated by INV-118 (C1-01 to C1-06, C1-13), INV-037 and INV-057 (SEC-3.4/D01).

### 3.5 Conditions of applicability

- A `when` clause and the antecedent of an invariant refer only to the output context (`ctx` or a context variable: audience, subject properties, the selected time range and periods), to `provides(K)`, and to other output elements. Subject properties are stated as Stage 1 states them ("the subject has migraine", "the subject menstruates"). How they become known is outside the model. They are not decision logic over input data.
- **Time frames.** Every context component states its time frame (E-007, E-008), because an output may concern periods long before the as-of date. A property of the subject's history (its headache types, treatment courses, acute medications, starts of withdrawal, available results) holds for every period up to the as-of date. A property of one treatment (its guidance types, the headache types it is given for, the IHS Q6 situation) is read for the treatment concerned. A property that changes with time (the spans during which the subject menstruates, the dates from which it is aged 12 and an adult) is read on the date or for the period that the invariant using it names.
- **Reference rule.** Where a Stage 1 statement includes another requirement's output by its ID (for example "migraine days (OUT-005)" in OUT-021), the component keeps the applicability condition of that requirement ("for patients with migraine"). Where a statement names a measure without such a reference (OUT-008, OUT-018, OUT-019, OUT-022, OUT-028, OUT-030, OUT-035), the model adds no condition that the statement does not state (see ISS-03 in section 8).
- **"Where provided".** Stage 1 phrases such as "where the corresponding outputs are provided" (OUT-021), "where OUT-010 is provided" (OUT-029) and "where reported" (OUT-018) are written `provides(K)`.
- **Audiences.** The Audience line of a Stage 1 requirement is stated in the catalogue (section 4.3, column Audience). It adds no constraint unless the Statement itself names an audience-specific output (OUT-025, OUT-034, OUT-035, OUT-036).

### 3.6 Summary outputs

Every `View` (E-003) is a summary output in the sense of OUT-001 and OUT-038: each view summarises diary information for a stated period.

### 3.7 Open world

An output may contain content that the model does not describe. Such content is an atom of `OtherItem` (E-004), so that the prohibitions of section 6, which constrain the `claims` of every element (E-001), apply to it as well. The model constrains what must, should or may be shown and what must not or should not be shown. It does not forbid other content.

### 3.8 Facts the context does not state (R-MCF)

The context may leave a fact unstated:

- the start of a treatment course (`startOf(c, t) = ∅`);
- the start of the treatment as it was first started (`originalStart(c, t) = ∅`);
- a course event of a kind (no target or tolerated dose reached, no end of a treatment cycle, no stop or pause);
- a selection (`previousConsultation`, `chosenPeriod` or `schemeSelection` empty, or fewer than two `comparedSpans`);
- an instrument or screening result (none available).

One rule applies to every such fact:

1. **Content aligned to the fact** is asked for only where the context states the fact, and is admitted only where the context states it. Such content is a period placed before or after the fact, a date or duration counted from it, or values compared at a time point counted from it. Its requirement has the antecedent `F ≠ ∅` (or quantifies over `F`), and its tie is `x ∈ F` or `∃ x ∈ F • …` in a definitional or MUST constraint.
2. **Content aligned to other facts of the same course** is asked for whether or not the context states the course's start. These facts are a stop, pause or dose reduction, the end of the course, and the as-of date. Where such content is bounded by the start ("on or after the start of the course"), the bound reads "on or after a dated course event of the course" (`courseBegunBy`, E-008). Where the start is stated, this is the same bound, because no course event precedes the start (INV-001). A summary of a period counts an acute course whose start is not stated as started (`courseNotOutside`, E-067).
3. **Selections.** Content for a selection is asked for, and admitted, only where the context makes the selection.
4. **Results.** A result is shown only where it is available. Content that rests on a result is asked for only where one is available ("Where results … are available", OUT-026, OUT-033).

In the model, "a treatment whose start the context states" replaces "a treatment that has started". Items that apply the rule cite "R-MCF (n)" in their Notes and do not restate it. The v34 places to which the rule applies are listed in `RATIONALE.md`, entry SEC-3.8/D01.

## 4. Model overview and output catalogue

### 4.1 Layers

The model has five layers.

1. **Frame** (E-001 to E-009). An `Output` is what a reader receives. It consists of one or more `View`s (summary outputs); each view covers a reporting `Period` and contains `Item`s, and every element carries the `claims` it puts to the reader. Every output is produced for an `OutputContext` (E-007, E-008); the repertoire `Rep` pairs outputs with contexts, and availability requirements are statements about `Rep` (section 3.2).
2. **Labels and reliability** (E-010, E-011, E-013). `Annotation`s (caveats, prompts, exploratory labels) qualify elements; `DefinitionLabel`s name the published definition of a measure; a `CompletenessIndicator` accompanies each reporting period.
3. **Per-period values** (E-012, E-014 to E-027, E-029 to E-031, E-033, E-051, E-064), the acute drug classes by which acute-medication days are broken down (E-028, not a `PeriodValue`), and the medication-overuse indicator (E-032, an item for one period and one class or combined use, not a `PeriodValue`). A `PeriodValue` is a value shown for one period and one type scope (all headache types combined, or one type).
4. **Views over time and treatment views** (E-034 to E-056): series with treatment markers, period comparisons, the response comparison with its changes, evaluation time points, residual burden, responder labels and adherence, the treatment review view, post-stop monitoring, the withdrawal follow-up view, acute-treatment effectiveness with per-attack lines, the treatment history and scheme windows.
5. **Instruments, special populations and audience-specific views** (E-057 to E-067): instrument and screening results with their value sets, the menstrual-relation view, cluster-headache outputs, the trigger co-occurrence view, the clinician-facing summary and the patient-facing overview.

Relations among the main kinds (→ is a reference, ⊂ is "part of"):

```
Output ⊃ View ⊃ Item
View.covers → Period;  PeriodValue.period → Period;  Series.periods → Period
Change.reference, Change.compared → DayCount
ResponseComparison → Period (baseline, on-treatment), DayCount, Change, EvaluationTimePoint
ResidualBurden → Change, DayCount;  ResponderLabel → ResponseComparison, ResidualBurden, Period, Item
MedicationOveruseIndicator → Period (reporting period, span), DayCount (basis)
AcuteTreatmentSummary → Period, TreatedAttackLine;  OutcomeSummary → AcuteTreatmentSummary
TreatmentHistoryView → ClassGroup → TreatmentLine → ResponseComparison | AcuteTreatmentSummary | AdherenceSummary
InstrumentResult → InstrumentResult (baseline administration)
Annotation → Element (qualified);  DefinitionLabel names the definition that its view follows for a measure
```

### 4.2 Catalogue: row IDs and columns

The catalogue (section 4.3) has one row per kind of output that a reader is shown. A row is identified by `OC-NN`; the constant `ocNN` of `enum CatalogueRow` (section 4.4) names the same row (`OC-07` ↔ `oc07`). The rows of the case tables of section 4.4 are identified by `C1-NN`, `C2-NN` and `C3-NN`, the rows of the source data tables of section 11 by `SD-<table>-NN`. These IDs are never renumbered or reused; a withdrawn row keeps its ID and is listed in section 9.

The catalogue table is an index. Its cells name items by ID, state levels, quote Stage 1 wording and repeat the OMN predicates of applicability conditions; they state no constraint of their own and have no formal force. The formal force of the catalogue lies in the enumeration `CatalogueRow` and in the case tables C1, C2 and C3 (section 4.4), over which the generic invariants INV-118, INV-119 and INV-120 quantify.

| Column | Content |
|---|---|
| Row | `OC-NN` |
| Output kind | the kind of output, as Stage 1 names it, and the element IDs |
| Audience | the Stage 1 Audience line(s) of the requirements realised, verbatim |
| Period and granularity | the periods the output refers to (formal in a C1 case or in the named invariant) |
| Applicability | the Stage 1 condition phrase and the OMN predicate that states it, or "R-MCF (n)" (section 3.8) |
| Availability | the level and the item that states it (`INV-NNN`, `C1-NN`), and the definitional invariants of the kind |
| Shown with it | companions, by ID: periods (INV-003), definition labels (INV-008, "label"), completeness (INV-011, "completeness"), placement markers (W2), C3 cases, specific companions, shown context facts (INV-123) |
| Prohibited | C2 cases, and INV-091 |
| Realises | the requirements whose statements name this kind of output; each is in the Realises field of an item named in the row |

Elements without a row of their own: E-001 (root; holds `claims`, `presents`, `factsShown`), E-007 and E-008 (context), E-009 (codes; values in table SD-IC), and E-014 (`DayCount`, whose kinds E-015 to E-018, E-020, E-021, E-029 and E-030 have rows; nesting in INV-122).

### 4.3 The catalogue

Abbreviations: "label" = INV-008, "completeness" = INV-011, "def." = definitional.

| Row | Output kind (elements) | Audience (Stage 1) | Period and granularity | Applicability | Availability | Shown with it | Prohibited | Realises |
|---|---|---|---|---|---|---|---|---|
| OC-01 | Summary output and its reporting period (E-002, E-003, E-004 `Item`, E-005) | OUT-001: patients, primary-care clinicians, specialists, researchers; OUT-038: patients, clinicians | the period each view covers | every output | structural; covered period MUST (E-003, INV-003); def. INV-002 | its periods (INV-003); caveats C3-01; completeness | C2-01 | OUT-001, OUT-034, OUT-035, OUT-038 |
| OC-02 | Time series of consecutive periods (E-006) | as the views that show it | calendar months, 28-day periods, calendar weeks | — | structural; def. INV-004 | its periods (INV-003) | — | OUT-001, OUT-004, OUT-009, OUT-015, OUT-028 |
| OC-03 | Definition label (E-011) | OUT-002: clinicians, researchers | per view | views that report the measure (`reports`) | SHOULD (INV-008); def. INV-111; fixed definitions (INV-125: SD-DF-01 MUST, SD-DF-02 SHOULD) | — | — | OUT-002, OUT-004, OUT-005, OUT-006, OUT-007, OUT-028 |
| OC-04 | Completeness indicator (E-013) | OUT-003: clinicians, researchers, patients | each reporting period of a summary measure | — | SHOULD (INV-011); def. INV-012, INV-121 | — | C2-02 | OUT-003, OUT-034 |
| OC-05 | Headache days (E-015; E-014) | OUT-004: patients, primary-care clinicians, specialists, researchers | per period; calendar month or 28-day period | every subject | MUST (C1-01); def. INV-006, INV-121, INV-122 | label (fixed: SD-DF-01); completeness | — | OUT-001, OUT-002, OUT-004 |
| OC-06 | Migraine days (E-016) | OUT-005: patients, clinicians, researchers | calendar month or 28-day period | "For patients with migraine" — `hasType(c, c1)` | MUST (C1-02) | label; completeness | — | OUT-001, OUT-002, OUT-005 |
| OC-07 | Moderate/severe headache days (E-017) | OUT-006: clinicians, researchers, patients | calendar month or 28-day period | every subject; MUST "where provided" — `provides(…)` | SHOULD (C1-03); MUST where provided (C1-04) | label; completeness | — | OUT-001, OUT-002, OUT-006 |
| OC-08 | Number of attacks (E-019 `AttackCount`) | OUT-007: clinicians, researchers | calendar month or 28-day period | every subject; MUST where provided | SHOULD (C1-05); MUST where provided (C1-06) | label (fixed: SD-DF-02); completeness | — | OUT-001, OUT-002, OUT-007 |
| OC-09 | Headache-free days, symptom-free days, periods without migraine days (E-020, E-021, E-022) | OUT-008: patients, clinicians, researchers | per reporting period | every subject (ISS-03) | MAY; SHOULD in the clinician-facing summary (INV-104; ISS-04); def. INV-031, INV-122 | exploratory label MAY (C3-02); label where a mark is shown; completeness | — | OUT-008 |
| OC-10 | Time-course view with treatment markers (E-034, E-035) | OUT-009: patients, clinicians, researchers | series of calendar months or 28-day periods; calendar weeks where weekly granularity is clinically relevant | every subject; weekly: `ctx.weeklyGranularityRelevant` | SHOULD (INV-034); content SHOULD (INV-035) | series and markers (W2 SHOULD, E-035); marker facts (INV-123) | — | OUT-009, OUT-034, OUT-035 |
| OC-11 | Intensity summary (E-023) | OUT-010: clinicians, patients | per reporting period | every subject | SHOULD (C1-07); between periods (INV-039, OC-33); def. INV-032, INV-121 | scale SHOULD (E-023); label where a distribution is shown | — | OUT-010, OUT-021, OUT-029, OUT-035 |
| OC-12 | Duration summary (E-024) | OUT-011: clinicians, patients | per reporting period | every subject | SHOULD (C1-08); def. INV-121 | "influenced by acute treatment" (C3-03) | C2-03 | OUT-011, OUT-013 |
| OC-13 | Associated symptoms and most bothersome symptom across periods (E-025, E-026) | OUT-012: clinicians, researchers, patients | per reporting period | "For migraine" — `hasType(c, c1)` | SHOULD (C1-09); def. INV-033, INV-121 | — | — | OUT-012, OUT-021 |
| OC-14 | Aura count and duration (E-027) | OUT-013: clinicians, patients | per reporting period | "patients with migraine with aura" — `hasType(c, c1_2)` | MAY (no invariant) | — | — | OUT-013 |
| OC-15 | Acute-medication days: total, per ICHD-3 8.2 class, per drug (E-028, E-029) | OUT-014: clinicians, patients, researchers | per reporting period | every subject; every acute medication used up to the as-of date (E-008) | MUST (C1-10); def. INV-024, INV-122; usage fact (INV-123) | completeness | — | OUT-014, OUT-015, OUT-016, OUT-029 |
| OC-16 | Weekly acute-medication view (E-036) | OUT-015: clinicians, patients | calendar weeks | every subject | SHOULD (C1-11) | completeness | — | OUT-015 |
| OC-17 | Medication-overuse indicator (E-032) | OUT-016: clinicians (primary), patients (in plain language) | calendar month or 28-day period, with its span | each class of the subject's acute medications; combined use | MUST (INV-044); def. INV-045, INV-046 | review prompt (C3-04 MUST); clinical-interpretation caveat (C3-05 SHOULD) | C2-04 | OUT-014, OUT-016, OUT-038 |
| OC-18 | Withdrawal follow-up view (E-039) | OUT-017: clinicians, patients | from the start of withdrawal; series of whole periods from it; NICE review window | "For patients withdrawing from overused medication": each start of withdrawal in `ctx.subject.withdrawalStart` | SHOULD (INV-049); content SHOULD (INV-050); def. INV-051 | series (W2 SHOULD); worsening label (C3-06); start fact (INV-123) | — | OUT-017 |
| OC-19 | Change from a reference period (E-040) | OUT-018: clinicians, patients, researchers; OUT-019: clinicians, patients | the two compared periods | wherever shown | def. INV-053; in a response comparison both forms MUST (E-040 `when`) | the two values, in a response comparison (W2 MUST); periods (INV-003); residual burden (INV-060); label; completeness | — | OUT-018, OUT-019, OUT-020, OUT-036 |
| OC-20 | Evaluation time point (E-041, E-042; SD-ER) | OUT-018: clinicians, patients, researchers | anchor date; date or window of evaluation | rules applicable to the treatment (`applicable`, E-041) | MUST with each response comparison (INV-059); def. INV-058 | — | — | OUT-018, OUT-036 |
| OC-21 | Response comparison (E-043) | OUT-018: clinicians, patients, researchers | baseline month; monthly on-treatment periods | "For each preventive treatment", whose start the context states — R-MCF (1) | MUST (INV-055); content MUST (INV-056, INV-057, INV-059) | values and changes (INV-003, INV-056, W2); time points (W2 MUST); adherence (INV-066); acute summaries per phase (INV-071); functional impact (INV-027); start fact (INV-123) | C2-05 | OUT-001, OUT-018, OUT-036 |
| OC-22 | Residual burden (E-044) | OUT-019: clinicians, patients | a calendar month or 28-day period within the compared period | "Wherever the output shows a relative (percentage) change in migraine or headache days" (compared period of at least 28 days: INV-060; ISS-13) | SHOULD (INV-060); def. INV-061 | — | — | OUT-019 |
| OC-23 | Responder label and its named criterion (E-045, E-046; SD-RC, SD-CL) | OUT-020: clinicians, patients | evaluated on-treatment periods | "If the output displays a responder or non-responder label" (MAY) | MAY; content SHOULD (INV-062); def. INV-063, INV-064, INV-114, INV-116 | comparison, residual burden, other values (W2 SHOULD); clinical-interpretation caveat (C3-07); treatment fact (INV-123) | C2-06 | OUT-020, OUT-025, OUT-038 |
| OC-24 | Days with migraine or moderate-to-severe headache, the count of the IHS position statement 2025 (E-018) | OUT-020: clinicians, patients | each evaluated month of a control-level label | with control-level labels | SHOULD with such a label (INV-062); def. INV-031 (relation to migraine days under `ihs2025MigraineDay`) | — | — | OUT-020 |
| OC-25 | Adherence summary (E-047) | OUT-039: clinicians, patients | an evaluation window of the response comparison | "For each preventive treatment" | SHOULD next to the comparison (INV-066), in the treatment history (INV-109), in the clinician-facing summary (INV-104); def. INV-067 | completeness of its window; treatment fact (INV-123) | — | OUT-039 |
| OC-26 | Treatment review view (E-048) | OUT-021: clinicians, patients | the same baseline and on-treatment periods | each preventive treatment whose start the context states — R-MCF (1) | MUST (INV-102); content MUST (INV-068), SHOULD where provided (INV-069) | treatment fact (INV-123) | — | OUT-021, OUT-023, OUT-036 |
| OC-27 | Post-stop monitoring view (E-049) | OUT-022: clinicians, patients | from the first changed day; on-treatment period; original baseline | each stop, pause or dose reduction of a preventive treatment, whether or not its start is stated — R-MCF (2) | SHOULD (INV-103); content SHOULD (INV-070, E-049 `when` clauses); def. INV-112 | event fact (INV-123) | — | OUT-022, OUT-036 |
| OC-28 | Acute-treatment summary, outcome summaries, treated-attack lines (E-050, E-051, E-052, E-053; SD-ET) | OUT-023: clinicians, patients | the selected time range; baseline and on-treatment periods; periods named by other rows | "For each acute medication" used up to the as-of date | SHOULD (INV-071); content SHOULD (INV-072, INV-073, INV-076); def. INV-074, INV-075 | outcome summaries and lines (W2 SHOULD); medication fact of lines (INV-123) | C2-07 | OUT-012, OUT-021, OUT-023, OUT-024, OUT-031 |
| OC-29 | Treatment history: view, class groups, treatment lines (E-054, E-055) | OUT-024: clinicians (primary), patients | the dates of each course | every treatment of the subject | SHOULD (INV-077); content SHOULD (INV-078, INV-109); def. INV-079 | groups (W2 SHOULD) and their lines (INV-078); response summaries and adherence (W2 SHOULD); course facts (INV-123) | — | OUT-024, OUT-034, OUT-039 |
| OC-30 | Scheme-window view (E-056) | OUT-025: clinicians preparing reimbursement or registry documentation | the selected windows | contexts with a scheme selection — R-MCF (3) | MAY; def. INV-080 | — | — | OUT-025 |
| OC-31 | Instrument result (E-057, E-058; SD-IN, SD-GB) | OUT-026: clinicians, patients, researchers | completion date | "Where results of validated instruments are available" — R-MCF (4) | SHOULD (INV-081); def. INV-082 | clinical-interpretation caveat where a category is shown (C3-08); availability fact (INV-123) | — | OUT-020, OUT-021, OUT-025, OUT-026, OUT-034, OUT-036, OUT-038 |
| OC-32 | Functional impact days (E-030) | OUT-027: clinicians, patients, researchers | per reporting period | every subject | SHOULD (C1-12); comparison with the baseline period SHOULD (INV-027); def. INV-121, INV-122 | — | — | OUT-027, OUT-036 |
| OC-33 | Comparison of selected periods (E-037) | OUT-001: patients, primary-care clinicians, specialists, researchers; OUT-010, OUT-027 | the selected periods | two or more selected periods — R-MCF (3) | MUST for equal lengths (INV-037); intensity SHOULD (INV-039); def. INV-038 | values in its view (INV-038 with INV-003) | — | OUT-001, OUT-010, OUT-027, OUT-036 |
| OC-34 | Three-month pattern view (E-038) | OUT-028: clinicians | the three most recent calendar months or 28-day periods | every context | MUST (INV-040); def. INV-041; definitions and codes SHOULD (INV-042) | series (W2, def.) | C2-08 | OUT-028, OUT-038 |
| OC-35 | Values per headache type (E-012, scopes `ofType`) | OUT-029: clinicians, patients | calendar month or 28-day period; intensity per period | "When the patient has, or may have, more than one headache type" — `#c.subject.possibleHeadacheTypes ≥ 2` | MUST (C1-13); intensity SHOULD where provided (C1-14); def. INV-122 | — | — | OUT-029 |
| OC-36 | Menstrual-relation view, cycle lines, attack marks (E-060, E-061) | OUT-030: clinicians, patients | consecutive cycles over the selected time range | "For patients who menstruate" — `menstruatesDuring(c, c.timeRange)` | MUST (INV-086); def. INV-087, INV-124 | attack marks (W2, def.); label; completeness | — | OUT-030, OUT-035 |
| OC-37 | Cluster-headache view, cluster and remission periods, attack rates (E-062, E-063, E-064) | OUT-031: clinicians, patients | the selected time range; bouts and remissions with their own dates | "For patients with cluster headache" — `hasType(c, c3_1)` | SHOULD (INV-088); def. INV-089, INV-124 | — (no placement: E-062/X01) | — | OUT-031 |
| OC-38 | Trigger co-occurrence view (E-065) | OUT-032: patients, clinicians | the covered period | — | MAY; def. INV-110 | caveats C3-09; label; completeness | — | OUT-001, OUT-032, OUT-038 |
| OC-39 | Screening result (E-059; SD-SC, SD-SR) | OUT-033: clinicians | its date | "Where results of depression or anxiety screening instruments … are available" — R-MCF (4) | SHOULD next to headache outputs (INV-083); def. INV-085 | clinical-interpretation caveat (C3-10); availability fact (INV-123) | C2-09 | OUT-033, OUT-038 |
| OC-40 | Clinician-facing summary (E-066) | OUT-034: primary-care clinicians, neurologists, headache specialists | a period chosen by the clinician (any dates); the period since the previous consultation | clinician audiences — `c.audience ∈ Clinicians` | SHOULD (INV-094); content SHOULD (INV-104) | — | — | OUT-034, OUT-039 |
| OC-41 | Patient-facing overview (E-067) | OUT-035: patients, parents and caregivers | any covered period | patient, parent and caregiver audiences | SHOULD (INV-095); content SHOULD (INV-105) | — | — | OUT-035 |
| OC-42 | Paediatric outputs: PedMIDAS, school days, caregiver impact, equal-length comparisons, supportive information (E-031; with E-030, E-058) | OUT-036: parents and caregivers, paediatric clinicians, researchers | periods that begin, and results completed, while the subject is a child or adolescent | "For children and adolescents" — `childOn`, `childIn` | SHOULD (INV-096, INV-097); def. INV-121 | supportive-information caveat (C3-11) | — | OUT-036 |
| OC-43 | Composite headache index (E-033) | OUT-037: clinicians, patients, researchers | per reporting period | "For migraine" (`concerns(…, c1)`); "for tension-type headache" (`concerns(…, c2)`) | no availability; content SHOULD (INV-092, INV-093); def. INV-115 | exploratory label (C3-12); components for migraine (W2 SHOULD) | SHOULD NOT primary for migraine (INV-091) | OUT-037 |
| OC-44 | Label or caveat (E-010) | as the element it qualifies | — | — | structural; asked by the C3 cells | shown with what it qualifies (W2, def., on `qualifies`) | — | OUT-008, OUT-011, OUT-016, OUT-017, OUT-032, OUT-036, OUT-037, OUT-038 |
| OC-45 | Other content (E-004 `OtherItem`) | any | — | — | permitted (section 3.7) | — | the C2 cells whose bearer is every element (C2-01, C2-02, C2-05, C2-07) | OUT-038 |

### 4.4 Formal columns of the catalogue

```omn
enum CatalogueRow ::= oc01 | oc02 | oc03 | oc04 | oc05 | oc06 | oc07 | oc08 | oc09 | oc10 | oc11 | oc12 | oc13 | oc14 | oc15
  | oc16 | oc17 | oc18 | oc19 | oc20 | oc21 | oc22 | oc23 | oc24 | oc25 | oc26 | oc27 | oc28 | oc29 | oc30 | oc31 | oc32
  | oc33 | oc34 | oc35 | oc36 | oc37 | oc38 | oc39 | oc40 | oc41 | oc42 | oc43 | oc44 | oc45     -- ocNN names row OC-NN
fun ppGranularities(r : CatalogueRow, l : Level) : set Granularity ≙ table C1 default ∅
fun ppRequired(r : CatalogueRow, l : Level, c : OutputContext) : set (TypeScope × set (ℙ PeriodValue)) ≙ table C1 default ∅
fun prohibitedClaims(r : CatalogueRow, l : Level) : set (ℙ Claim × ℙ Element) ≙ table C2 default ∅
fun requiredAnnotations(r : CatalogueRow, l : Level) : set (AnnotationKind × ℙ Element) ≙ table C3 default ∅
```

`ppGranularities(r, l)` and `ppRequired(r, l, c)` give the cases of per-period availability read by INV-118: a set of granularities, and, for a context c, pairs of a type scope and kinds of per-period value that one view and one series show together for every period of the selected time range. `prohibitedClaims(r, l)` gives the cases read by INV-119: pairs of a set of claims and a set of elements, the bearers. `requiredAnnotations(r, l)` gives the cases read by INV-120: pairs of an annotation kind and a set of elements, the bearers. In a cell, `ctx(outputOf(x))` is the context of the output of x, which is `ctx` in an output-scope invariant (section 2.9). The v34 origin of each case is stated in the `RATIONALE.md` entries C1-NN/D01, C2-NN/D01 and C3-NN/D01.

Case table C1 — form C: cases of `ppGranularities` and `ppRequired` (per-period availability, read by INV-118)

| Row | `r : CatalogueRow` | `l : Level` | `ppGranularities(r, l)` | `ppRequired(r, l, c)` | Stage 1 part |
|---|---|---|---|---|---|
| C1-01 | `oc05` | `must` | `MonthlyKind` | `{(allTypes, {HeadacheDays})}` | OUT-001 (MUST), OUT-004 (MUST) |
| C1-02 | `oc06` | `must` | `MonthlyKind` | `{q ∈ {(allTypes, {MigraineDays})} \| hasType(c, c1)}` | OUT-001, OUT-005 (MUST) |
| C1-03 | `oc07` | `should` | `MonthlyKind` | `{(allTypes, {ModerateSevereHeadacheDays})}` | OUT-006 (SHOULD) |
| C1-04 | `oc07` | `must` | `MonthlyKind` | `{q ∈ {(allTypes, {ModerateSevereHeadacheDays})} \| provides(ModerateSevereHeadacheDays)}` | OUT-001 (MUST) |
| C1-05 | `oc08` | `should` | `MonthlyKind` | `{(allTypes, {AttackCount})}` | OUT-007 (SHOULD) |
| C1-06 | `oc08` | `must` | `MonthlyKind` | `{q ∈ {(allTypes, {AttackCount})} \| provides(AttackCount)}` | OUT-001 (MUST) |
| C1-07 | `oc11` | `should` | `Granularity` | `{(allTypes, {{m : IntensitySummary \| m.scale ≠ ∅}})}` | OUT-010 (SHOULD) |
| C1-08 | `oc12` | `should` | `Granularity` | `{(allTypes, {{m : DurationSummary \| m.kind ≠ auraDuration}})}` | OUT-011 (SHOULD) |
| C1-09 | `oc13` | `should` | `Granularity` | `{q : TypeScope × set (ℙ PeriodValue) \| hasType(c, c1) ∧ (q = (allTypes, {MostBothersomeSymptomItem}) ∨ ∃ s : AssociatedSymptom • q = (allTypes, {{m : AssociatedSymptomSummary \| m.symptom = s}}))}` | OUT-012 (SHOULD) |
| C1-10 | `oc15` | `must` | `Granularity` | `{(allTypes, medicationKinds(c))}` | OUT-014 (MUST) |
| C1-11 | `oc16` | `should` | `{calendarWeek}` | `{(allTypes, {TotalAcuteMedicationDays})}` | OUT-015 (SHOULD) |
| C1-12 | `oc32` | `should` | `Granularity` | `{(allTypes, {fiDays(paidWorkOrSchool, affected), fiDays(householdWork, affected), fiDays(socialOrLeisure, affected), {m : DayCount \| ∃ d : ImpactDomain • m.measure = functionalImpactDays((d, severelyImpaired))}})}` | OUT-027 (SHOULD) |
| C1-13 | `oc35` | `must` | `MonthlyKind` | `{q : TypeScope × set (ℙ PeriodValue) \| #c.subject.possibleHeadacheTypes ≥ 2 ∧ q.1 ∈ {allTypes} ∪ {t ∈ c.subject.possibleHeadacheTypes • ofType(t)} ∧ q.2 = {HeadacheDays} ∪ medicationKinds(c) ∪ {K ∈ {ModerateSevereHeadacheDays, AttackCount} \| provides(K)}}` | OUT-029 (MUST) |
| C1-14 | `oc35` | `should` | `Granularity` | `{q : TypeScope × set (ℙ PeriodValue) \| #c.subject.possibleHeadacheTypes ≥ 2 ∧ provides(IntensitySummary) ∧ q.2 = {IntensitySummary} ∧ ∃ t ∈ c.subject.possibleHeadacheTypes • q.1 = ofType(t)}` | OUT-029 (SHOULD, where OUT-010 is provided) |

Case table C2 — form C: cases of `prohibitedClaims` (read by INV-119)

| Row | `r : CatalogueRow` | `l : Level` | `prohibitedClaims(r, l)` | Stage 1 part |
|---|---|---|---|---|
| C2-01 | `oc01` | `shouldNot` | `{({x : Claim \| x = replacesClinicalAssessment ∨ ∃ d : DiagnosisRef • x = diagnosis(d)}, Element)}` | OUT-038 (SHOULD) |
| C2-02 | `oc04` | `shouldNot` | `{({clinicallyValidatedCutoff}, Element)}` | OUT-003 (SHOULD NOT) |
| C2-03 | `oc12` | `shouldNot` | `{({standAloneEfficacyMeasure}, {d : DurationSummary \| d.kind ≠ auraDuration ∧ d.attackScope ≠ untreatedAttacks})}` | OUT-011 Caveat (SHOULD) |
| C2-04 | `oc17` | `mustNot` | `{({x : Claim \| ∃ t : ICHD3Code • t ⊑ c8_2 ∧ x = diagnosis(headacheDiagnosis(t))}, MedicationOveruseIndicator)}` | OUT-016 (MUST NOT) |
| C2-05 | `oc21` | `mustNot` | `{({continuationDecision}, Element)}` | OUT-018 Caveat (MUST); OUT-020 Rationale (second part) |
| C2-06 | `oc23` | `shouldNot` | `{({soleIndicatorOfIndividualBenefit}, ResponderLabel)}` | OUT-020 (SHOULD NOT) |
| C2-07 | `oc28` | `shouldNot` | `{({acuteResponseDefinitionDecision}, Element)}` | OUT-023 Caveat (SHOULD) |
| C2-08 | `oc34` | `shouldNot` | `{({x : Claim \| ∃ d : DiagnosisRef • x = diagnosis(d)}, {x : Element \| x ∈ ThreeMonthPatternView ∨ ∃ v : ThreeMonthPatternView • x ∈ v.content})}` | OUT-028 (SHOULD NOT) |
| C2-09 | `oc39` | `shouldNot` | `{({x : Claim \| ∃ y : Text • x = diagnosis(psychiatricDiagnosis(y))}, ScreeningResult)}` | OUT-033 Caveat (SHOULD) |

Case table C3 — form C: cases of `requiredAnnotations` (read by INV-120)

| Row | `r : CatalogueRow` | `l : Level` | `requiredAnnotations(r, l)` | Stage 1 part |
|---|---|---|---|---|
| C3-01 | `oc01` | `should` | `{(patientReportedDiaryInformation, View), (supportsDoesNotReplaceClinicalAssessment, View)}` | OUT-038 (SHOULD) |
| C3-02 | `oc09` | `may` | `{(exploratoryMeasure, HeadacheFreeDays ∪ SymptomFreeDays ∪ MigraineFreePeriodMark)}` | OUT-008 (MAY) |
| C3-03 | `oc12` | `should` | `{(durationInfluencedByAcuteTreatment, {d : DurationSummary \| d.kind ≠ auraDuration ∧ d.attackScope ≠ untreatedAttacks})}` | OUT-011 (SHOULD) |
| C3-04 | `oc17` | `must` | `{(reviewPromptPossibleMedicationOveruse, MedicationOveruseIndicator)}` | OUT-016 (MUST) |
| C3-05 | `oc17` | `should` | `{(requiresClinicalInterpretation, MedicationOveruseIndicator)}` | OUT-038 (SHOULD) |
| C3-06 | `oc18` | `should` | `{(expectedTransientWorseningEarlyWithdrawal, WithdrawalFollowUpView)}` | OUT-017 (SHOULD) |
| C3-07 | `oc23` | `should` | `{(requiresClinicalInterpretation, ResponderLabel)}` | OUT-038 |
| C3-08 | `oc31` | `should` | `{(requiresClinicalInterpretation, {r : InstrumentResult \| r.category ≠ ∅})}` | OUT-038, OUT-026 |
| C3-09 | `oc38` | `should` | `{(coOccurrenceNotCausation, TriggerCooccurrenceView), (apparentTriggersMayBePremonitorySymptoms, TriggerCooccurrenceView), (requiresClinicalInterpretation, TriggerCooccurrenceView)}` | OUT-032 (caveats SHOULD), OUT-038 |
| C3-10 | `oc39` | `should` | `{(requiresClinicalInterpretation, ScreeningResult)}` | OUT-038, OUT-033 |
| C3-11 | `oc42` | `should` | `{(supportiveInformation, {v : View \| childIn(ctx(outputOf(v)), {v.covers} ∪ (v.content ∩ Period)) ∨ ∃ r ∈ v.content ∩ InstrumentResult; d ∈ r.completionDate • childOn(ctx(outputOf(v)), d)})}` | OUT-036 Caveat (SHOULD) |
| C3-12 | `oc43` | `should` | `{(exploratoryMeasure, {x : CompositeIndex \| concerns(ctx(outputOf(x)), x.typeScope, c1)})}` | OUT-037 (SHOULD) |

## 5. Model elements

### 5.1 Frame: outputs, views, periods and context

### E-001 Element
- Definition:
```omn
abstract element Element {
  claims : set Claim  core      -- the interpretive claims the element puts to its reader by its wording or presentation
}
variant Claim ::= diagnosis ⟨DiagnosisRef⟩      -- presents the subject as having this diagnosis
  | clinicallyValidatedCutoff                    -- presents a fixed completeness cut-off as clinically validated
  | soleIndicatorOfIndividualBenefit             -- presents itself as the sole indicator of individual benefit
  | standAloneEfficacyMeasure                    -- presents itself as a stand-alone measure of treatment efficacy
  | replacesClinicalAssessment                   -- presents itself as replacing clinical assessment or diagnosis
  | continuationDecision                         -- presents a decision to continue, stop or change a preventive treatment
  | acuteResponseDefinitionDecision              -- presents one definition of acute treatment response as the one that applies
variant DiagnosisRef ::= headacheDiagnosis ⟨ICHD3Code⟩ | psychiatricDiagnosis ⟨Text⟩
-- presents(x, C): x is presented with the claim C, by its own wording or by an annotation that qualifies it (INV-119)
pred presents(x : Element, C : Claim) ≙ C ∈ x.claims ∨ ∃ a : Annotation • x ∈ a.qualifies ∧ C ∈ a.claims
-- factsShown(x): the facts of the context that the element x shows (INV-123)
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
- Meaning: The root of all output elements. `claims` states, abstractly, what an element asserts to its reader beyond the values it shows, for example that its content is a diagnosis. An empty `claims` set is the normal case.
- Conformance: Structural; `claims` is core. Definitional: INV-123 (`factsShown`). Prohibited: INV-119 (C2-01 to C2-09).
- Realises: OUT-003, OUT-011, OUT-016, OUT-018, OUT-020, OUT-023, OUT-028, OUT-033, OUT-038
- Evidence: Stage 1 OUT-003, OUT-011 (Caveats), OUT-016, OUT-018 (Caveats), OUT-020, OUT-023 (Caveats), OUT-028, OUT-033 (Caveats), OUT-038.
- Notes: Rationale: E-001/D01.

### E-002 Output
- Definition:
```omn
element Output extends Element {
  views : set1 View  core       -- the views the reader receives together (composition)
}
fun outputOf : Element → Output     -- the output an element belongs to (section 2.5): an output belongs to itself, a view to the
                                    --   output of which it is a part, and an item to the output of its view
```
- Meaning: What one reader receives at one time (for example a consultation summary, a chart or a report), produced for one context (`ctx(o)`, section 3.2).
- Conformance: Structural.
- Realises: OUT-001, OUT-038
- Evidence: Stage 1 OUT-001, OUT-038.

### E-003 View
- Definition:
```omn
element View extends Element {
  covers : →Period  MUST                       -- the reporting period the view covers (start, end, length)
  content : set Item  core                     -- the items shown in the view (composition)
  qualities : set PresentationQuality  core    -- presentation qualities the view has
}
enum PresentationQuality ::= plainLanguage | concise
fun viewOf : Item → View                        -- the view an item is part of (section 2.5)
```
- Meaning: A summary output (section 3.6): a coherent presentation of diary information for a stated reporting period, such as a chart, a table, a summary or an overview. Items shown "together", "next to" or "in the same view" are parts of the same view. `qualities` lists the presentation qualities that Stage 1 requires of particular views (plain language, OUT-035; concise, OUT-034).
- Conformance: Structural; the view kinds state their availability in the elements that extend View. Content: INV-003 (MUST); INV-008, INV-011 (SHOULD). Labels and caveats: C3-01, C3-11.
- Realises: OUT-001, OUT-034, OUT-035, OUT-038
- Evidence: Stage 1 OUT-001, OUT-034, OUT-035, OUT-038.
- Notes: Relations: INV-003. Rationale: E-003/D01.

### E-004 Item and OtherItem
- Definition:
```omn
abstract element Item extends Element { }
element OtherItem extends Item {
  description : Text  core      -- content the model does not describe further
}
```
- Meaning: `Item` is anything shown inside a view. `OtherItem` is content outside the model's element types (section 3.7), so that prohibitions apply to it.
- Conformance: Structural (`OtherItem`: section 3.7). Prohibited: the C2 cases whose bearer is every element (C2-01, C2-02, C2-05, C2-07).
- Realises: OUT-038
- Evidence: Stage 1 OUT-038.

### E-005 Period
- Definition:
```omn
element Period extends Item {
  start : Date  MUST                 -- first day of the period
  end : Date  MUST                   -- last day of the period
  lengthDays : ℕ₁  derived MUST      -- number of days of the period; unit: days
  kind : PeriodKind  core
}
enum PeriodKind ::= calendarMonth | fourWeekPeriod | calendarWeek | otherSpan
type Granularity == {calendarMonth, fourWeekPeriod, calendarWeek}
type MonthlyKind == {calendarMonth, fourWeekPeriod}
pred ofKind(d₁ : Date, d₂ : Date, k : PeriodKind) ≙
  (k = calendarMonth ⇒ isMonthSpan(d₁, d₂)) ∧ (k = fourWeekPeriod ⇒ days(d₁, d₂) = 28) ∧
  (k = calendarWeek ⇒ isWeekSpan(d₁, d₂))
pred within(p : Period, q : Period) ≙ q.start ≤ p.start ∧ p.end ≤ q.end
pred inPeriod(d : Date, p : Period) ≙ p.start ≤ d ∧ d ≤ p.end
fun spanOf(p : Period) : DateSpan ≙ DateSpan(from ↦ p.start, to ↦ p.end)
pred sameSpan(p : Period, r : DateSpan) ≙ p.start = r.from ∧ p.end = r.to
pred equalLengths(ps : set →Period) ≙ ∀ p, q ∈ ps • p.lengthDays = q.lengthDays
```
- Meaning: A reporting period stated with its start date, end date and length in days. `fourWeekPeriod` is the 28-day (4-week) period of ICHD-3 and the IHS trial guidelines; `calendarMonth` a calendar month; `calendarWeek` a calendar week; `otherSpan` any other stated span (for example a baseline period, a time since the previous consultation, a scheme window).
- Conformance: Structural. Definitional: INV-002.
- Realises: OUT-001
- Evidence: Stage 1 OUT-001.
- Notes: Relations: INV-002.

### E-006 Series
- Definition:
```omn
element Series extends Item {
  periods : seq1 →Period  core       -- consecutive reporting periods, earliest first
  granularity : Granularity  core
}
pred consecutive(s : seq →Period) ≙ ∀ i ∈ dom s • i < #s ⇒ s(i + 1).start = next(s(i).end)
pred tiles(sr : Series, r : DateSpan, g : Granularity) ≙
  sr.granularity = g ∧ first(sr.periods).start = r.from ∧ last(sr.periods).end = r.to
pred perPeriod(v : View, sr : Series, K : ℙ PeriodValue, sc : TypeScope) ≙
  ∀ p ∈ ran sr.periods • ∃ m ∈ v.content ∩ K • m.period = p ∧ m.typeScope = sc
pred containsPeriodOf(r : DateSpan, g : Granularity) ≙
  ∃ d₁, d₂ : Date • r.from ≤ d₁ ∧ d₁ ≤ d₂ ∧ d₂ ≤ r.to ∧ ofKind(d₁, d₂, g)
pred fillsPeriod(sr : Series, p : Period) ≙
  within(first(sr.periods), p) ∧ within(last(sr.periods), p) ∧
  (sr.granularity = fourWeekPeriod ⇒ first(sr.periods).start = p.start) ∧   -- 28-day periods are counted from the first day of p
  ¬ ∃ d₁, d₂ : Date • p.start ≤ d₁ ∧ d₁ ≤ d₂ ∧ d₂ ≤ p.end ∧ ofKind(d₁, d₂, sr.granularity) ∧
      (d₂ < first(sr.periods).start ∨ last(sr.periods).end < d₁)
```
- Meaning: A time series of consecutive reporting periods of one granularity (calendar months, 28-day periods or calendar weeks), used whenever values are shown "for every period in the selected time range" or "as a time series of consecutive reporting periods". `containsPeriodOf(r, g)` holds when the span r contains a whole period of granularity g: a whole calendar month, 28 consecutive days, or a whole calendar week. `fillsPeriod(sr, p)` holds when the series lies within the period p, begins on the first day of p if its periods are 28-day periods, and leaves no whole period of its granularity within p before its first or after its last period, so that it consists of all whole periods of its granularity within p: the whole calendar months or the whole calendar weeks within p, or the consecutive 28-day periods from the first day of p that end within p. Calendar months and calendar weeks follow the calendar, so p fixes which of them lie within it. 28-day periods do not follow the calendar, so they are counted from the first day of p, as the periods of the selected time range are counted from its first day (INV-001); the series then leaves fewer than 28 days of p after its last period and none before its first.
- Conformance: Structural; it takes the level of the views that use it. Definitional: INV-004.
- Realises: OUT-001, OUT-004, OUT-009, OUT-015, OUT-028
- Evidence: Stage 1 OUT-001, OUT-004, OUT-009, OUT-015, OUT-028.
- Notes: Relations: INV-004. Rationale: E-006/D01.

### E-007 OutputContext
- Definition:
```omn
value OutputContext {
  audience : Audience                     -- the reader the output is produced for, as of the as-of date
  subject : SubjectProfile                -- the person the output is about (E-008)
  asOf : Date                             -- the date as of which the output is produced
  timeRange : DateSpan                    -- the time range selected for the output
  granularity : Granularity               -- the period granularity selected for series
  comparedSpans : seq DateSpan            -- periods selected for comparison (may be empty)
  previousConsultation : opt Date         -- the date of the subject's most recent consultation on or before the as-of date, if any
  chosenPeriod : opt DateSpan             -- a period chosen by the clinician for the clinician-facing summary, any dates
  schemeSelection : opt SchemeSelection   -- evaluation windows of a reimbursement or monitoring scheme selected by a clinician
  weeklyGranularityRelevant : 𝔹           -- weekly granularity is clinically relevant for this output, as of the as-of date
}
enum Audience ::= adultPatient | parentOrCaregiver | primaryCareClinician | headacheSpecialist | researcherOrRegistry
const Clinicians : set Audience ≙ {primaryCareClinician, headacheSpecialist}
value SchemeSelection { scheme : SchemeName; windows : seq1 DateSpan }
given SchemeName                          -- the name of a national reimbursement or monitoring scheme, as an output labels it
```
- Meaning: The context for which an output is produced: who reads it, whom it is about, as of which date, for which selected time range and granularity, and which periods or windows the reader selected. Stage 1 refers to these as the selected time range (OUT-004), periods to be compared (OUT-001), a period chosen by the clinician (OUT-034), and evaluation windows selected by the clinician (OUT-025). `weeklyGranularityRelevant` is the OUT-009 condition "where weekly granularity is clinically relevant (tension-type headache, cluster headache, early onset of effect)". Audiences are those of Stage 1 section 2; clinicians preparing reimbursement documentation and paediatric clinicians are clinicians. **Time frames.** The audience and `weeklyGranularityRelevant` are properties of the output, as of the as-of date; they hold for every period the output shows. The previous consultation is the subject's most recent consultation on or before the as-of date, so that "the period since the previous consultation" (OUT-034) ends on the as-of date; an earlier period between consultations is a period chosen by the clinician. The selected time range, the comparison periods, the chosen period and the scheme windows are dated spans. The subject's properties and their time frames are stated in E-008.
- Conformance: Structural (a semantic parameter, not an output element). Context invariant: INV-001.
- Realises: OUT-001, OUT-004, OUT-009, OUT-025, OUT-034, OUT-035, OUT-036
- Evidence: Stage 1 section 2 (Audiences), OUT-001, OUT-004, OUT-009, OUT-025, OUT-034.
- Notes: Rationale: E-007/D01.

### E-008 SubjectProfile
- Definition:
```omn
value SubjectProfile {
  headacheTypes : set HeadacheType               -- the headache types the subject has, or has had, at any time up to the as-of date
  possibleHeadacheTypes : set HeadacheType       -- the headache types the subject has or may have, or has had or may have had,
                                                 --   at any time up to the as-of date
  menstruationSpans : set DateSpan               -- the spans of time, up to the as-of date, during which the subject menstruates
                                                 --   (has menstrual cycles); a span that continues on the as-of date ends on it
  adultFrom : Date                               -- the first day on which the subject is an adult; before it, the subject is a child
                                                 --   or adolescent; it may lie after the as-of date
  aged12From : Date                              -- the subject's twelfth birthday; it may lie after the as-of date
  preventiveTreatments : set Treatment           -- every preventive treatment course of the subject up to the as-of date, ongoing or stopped
  acuteTreatments : set Treatment                -- every acute treatment course of the subject up to the as-of date, ongoing or stopped
  preventiveTypes : set (Treatment × PreventiveTreatmentType)   -- how current guidance classifies each preventive treatment
  preventiveFor : set (Treatment × HeadacheType) -- the headache type or types each preventive treatment is given for (for its course)
  acuteMedications : set AcuteMedication         -- every acute medication (drug and formulation) the subject has used at any time up to
                                                 --   the as-of date; a medication stays in the set after its use has stopped
  courseEvents : set CourseEvent                 -- start, dose changes, target dose, treatment cycles and stop of each treatment, each dated
  resumes : set (Treatment × Treatment)          -- (t₁, t₂): the preventive treatment course t₂ resumes the treatment of the course t₁
                                                 --   after the stop or pause of t₁
  withdrawalStart : set Date                     -- every start of withdrawal of overused medication up to the as-of date
  ihsQ6ChronicAlternative : set Treatment        -- the preventive treatments to which the IHS 2024 Q6 situation applies: chronic migraine
                                                 --   without a ≥ 50% decrease after multiple preventive options
  instrumentAdministrations : set InstrumentAdministration   -- results of validated instruments that are available, each with its date
  screeningAdministrations : set ScreeningAdministration     -- results of comorbidity screening instruments that are available, each with its date
}
given Treatment, Drug, FormulationOrRoute
fun drugOf : Treatment → Drug                    -- the medication of a treatment course
value AcuteMedication { drug : Drug; formulation : FormulationOrRoute }
value CourseEvent { treatment : Treatment; kind : CourseEventKind; date : Date }
variant CourseEventKind ::= start | doseChange ⟨DoseChangeDirection⟩ | targetDoseReached
  | cycleEnd ⟨ℕ₁⟩ | stop ⟨StopKind⟩
enum DoseChangeDirection ::= increase | reduction
enum StopKind ::= discontinued | paused
enum PreventiveTreatmentType ::= doseTitratedPreventive | fixedDosePreventive | oralPreventive | cgrpInhibitor
  | antiCGRPMonoclonalAntibody | monthlyInjectable | quarterlyInjectable | onabotulinumtoxinA | otherPreventive
value InstrumentAdministration { instrument : Instrument; date : Date }
value ScreeningAdministration { instrument : ScreeningInstrument; date : Date }
pred hasType(c : OutputContext, t : ICHD3Code) ≙ ∃ h ∈ c.subject.headacheTypes • h ⊑ t
pred mayHaveType(c : OutputContext, t : ICHD3Code) ≙ ∃ h ∈ c.subject.possibleHeadacheTypes • h ⊑ t
pred eventOn(c : OutputContext, t : Treatment, k : CourseEventKind, d : Date) ≙
  CourseEvent(treatment ↦ t, kind ↦ k, date ↦ d) ∈ c.subject.courseEvents
fun startOf(c : OutputContext, t : Treatment) : set Date ≙
  {e ∈ c.subject.courseEvents | e.treatment = t ∧ e.kind = start • e.date}     -- at most one member (INV-001)
-- courseBegunBy(c, t, d): a course event of treatment t is dated on or before d, so that the context places the course of t as
-- begun by d; where the context states the start, this holds exactly for the days on or after it (no course event precedes it)
pred courseBegunBy(c : OutputContext, t : Treatment, d : Date) ≙ ∃ e ∈ c.subject.courseEvents • e.treatment = t ∧ e.date ≤ d
-- resumesFrom(c, u, t): t is u, or the course t resumes the treatment of the course u, directly or through courses that each
-- resume the treatment of the course before them
pred resumesFrom(c : OutputContext, u : Treatment, t : Treatment) ≙
  ∃ s : seq1 Treatment • first(s) = u ∧ last(s) = t ∧ ∀ i ∈ dom s • i < #s ⇒ (s(i), s(i + 1)) ∈ c.subject.resumes
-- originalStart(c, t): the start of the treatment of course t as it was first started: the start that the context states for the
-- first course of the chain of courses that t resumes (resumesFrom), the one that resumes no course; ∅ where the context states no
-- start for that course; at most one member
fun originalStart(c : OutputContext, t : Treatment) : set Date ≙
  {d : Date | ∃ u : Treatment • resumesFrom(c, u, t) ∧ (∀ p ∈ c.subject.resumes • p.2 ≠ u) ∧ d ∈ startOf(c, u)}
pred givenFor(c : OutputContext, t : Treatment, h : ICHD3Code) ≙ ∃ k : HeadacheType • (t, k) ∈ c.subject.preventiveFor ∧ k ⊑ h
pred childOn(c : OutputContext, d : Date) ≙ d < c.subject.adultFrom          -- the subject is a child or adolescent on d
pred childIn(c : OutputContext, ps : set →Period) ≙ ∃ p ∈ ps • childOn(c, p.start)
pred menstruatesDuring(c : OutputContext, r : DateSpan) ≙ ∃ s ∈ c.subject.menstruationSpans • s.from ≤ r.to ∧ r.from ≤ s.to
-- ShownFact: a fact of the context that an element shows (factsShown, E-001; INV-123)
variant ShownFact ::= preventiveCourse ⟨Treatment⟩ | acuteCourse ⟨Treatment⟩ | courseEvent ⟨CourseEvent⟩
  | stopOn ⟨Treatment × Date⟩ | stoppedCourse ⟨Treatment⟩ | withdrawal ⟨Date⟩
  | usedMedication ⟨Drug × set FormulationOrRoute⟩ | usedScope ⟨MedicationScope⟩
  | availableResult ⟨Instrument × set Date⟩ | availableScreening ⟨ScreeningInstrument × set Date⟩
pred inMedicationScope(m : AcuteMedication, s : MedicationScope) ≙ s = allAcuteMedication ∨ s = ofClass(classOf(m.drug)) ∨
  s = ofDrug(m.drug) ∨ (∃ ks : set1 AcuteDrugClass • s = ofClasses(ks) ∧ classOf(m.drug) ∈ ks)
-- stated(c, f): the context c states the fact f
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
- Meaning: The properties of the output's subject on which Stage 1 conditions depend, stated as Stage 1 states them, each with its time frame. An output may concern periods long before the as-of date, so a property that held in such a period keeps its effect there. There are three time frames:
  - **The subject's history up to the as-of date.** A property that held at any time up to the as-of date holds for every period an output shows:
    - the headache types the subject has or has had (`headacheTypes`), and those it has or may have, or has had or may have had (`possibleHeadacheTypes`) (OUT-005, OUT-012, OUT-013, OUT-029, OUT-031, OUT-037);
    - every preventive and every acute treatment course, ongoing or stopped, with its course events (start, dose change, the date the target or tolerated dose was reached, the end of treatment cycles, stop or pause), each dated on or before the as-of date under the day convention of section 2.8: the start on the first day of the course; a dose change, and the reaching of the target or tolerated dose, on the first day at the new dose; the end of treatment cycle n (`cycleEnd(n)`) on the first day after that cycle, the day by which the cycle is complete; and a stop or pause, at most one for each course (INV-001), on the last day of the course (OUT-009, OUT-018, OUT-022, OUT-023, OUT-024, OUT-031, OUT-039); and, for each preventive treatment course that resumes the treatment of an earlier course after its stop or pause, the course it resumes (`resumes`; OUT-022);
    - every acute medication, drug and formulation or route, that the subject has used (`acuteMedications`; OUT-014, OUT-016, OUT-021, OUT-023). A medication stays in the set after its use has stopped, so that the totals, classes and drugs of OUT-014, the class indicators of OUT-016 and the per-drug summaries of OUT-023 are given for periods in which a medication that the subject no longer uses was taken;
    - every start of withdrawal of overused medication (OUT-017);
    - every available instrument and screening result, each with its date (OUT-026, OUT-033, OUT-036).
  - **One treatment.** A property of a preventive treatment course holds for that course: its guidance types (`preventiveTypes`); the headache type or types it is given for (`preventiveFor`), for example a preventive treatment of chronic migraine, of tension-type headache or of cluster headache; and whether the IHS 2024 Q6 situation applies to it (`ihsQ6ChronicAlternative`). `givenFor(c, t, h)` holds when t is given for h or a subtype of h. The conditions of responder criteria that concern the subject's migraine ("in episodic migraine", "in chronic migraine", the IHS Q6 situation) are read on the treatment a label refers to (E-045), not on the headache types the subject has had at other times.
  - **Dated properties.** A property that changes with time is read on the date, or for the period, that the invariant using it names:
    - the spans during which the subject menstruates (`menstruationSpans`; OUT-030, OUT-035). `menstruatesDuring(c, r)` holds when such a span overlaps r;
    - the first day on which the subject is an adult (`adultFrom`). Before it the subject is a child or adolescent (OUT-036; also the population of the Russian clinical recommendations for children, OUT-018, E-041). `childOn(c, d)` holds when the subject is a child or adolescent on d, and `childIn(c, ps)` when it is one on the first day of one of the periods ps;
    - the subject's twelfth birthday (`aged12From`), from which NICE CG150 covers young people (OUT-018, E-041).

  A dose reduction (`doseChange(reduction)`) is the "reduced" of OUT-022 and a pause (`stop(paused)`) its "paused". `resumesFrom(c, u, t)` holds when t is u or resumes the treatment of u, directly or through courses that each resume the treatment of the course before them. `courseBegunBy(c, t, d)` holds when a course event of t is dated on or before d, so that the context places the course of t as begun by d: every course event is dated on or after the day its course began (section 2.8), and, where the context states the start, the predicate holds exactly for the days on or after that start, because no course event precedes the start (INV-001). How these properties become known is outside the model.
- Conformance: Structural (a semantic parameter). Context invariant: INV-001. Definitional: INV-123 (`stated`).
- Realises: OUT-005, OUT-009, OUT-012, OUT-013, OUT-014, OUT-016, OUT-017, OUT-018, OUT-020, OUT-021, OUT-022, OUT-023, OUT-024, OUT-026, OUT-029, OUT-030, OUT-031, OUT-033, OUT-035, OUT-036, OUT-037, OUT-039
- Evidence: Stage 1 statements of the requirements listed; [S-008], [S-011], [S-014], [S-015], [S-022] E-008/Q00.
- Notes: `PreventiveTreatmentType` lists the treatment types to which the guidance time points of E-041 refer (Stage 1 OUT-018: "which differ by treatment type"). `cgrpInhibitor` is the NICE CG150 term; `oralPreventive`, `monthlyInjectable` and `quarterlyInjectable` are the IHS 2024 Q2 categories (oral preventive treatment, injectable drugs taken on a monthly basis, injectable drugs administered quarterly; E-041). A treatment may have several types, and `preventiveTypes` lists each type that describes it: for example, topiramate is `doseTitratedPreventive` and `oralPreventive`; an oral CGRP receptor antagonist is `fixedDosePreventive`, `cgrpInhibitor` and `oralPreventive`; a course of onabotulinumtoxinA is `onabotulinumtoxinA` and `quarterlyInjectable`. Every preventive treatment has at least one type (INV-001): `otherPreventive` is the type of a preventive treatment that none of the other values describes. Rationale: E-008/D01, E-008/D02, E-008/D03, E-008/D04.

### E-009 ICHD-3 code references
- Definition:
```omn
given ICHD3Code
type HeadacheType == ICHD3Code
fun label : ICHD3Code → Text                  -- the code and its name as printed in ICHD-3
fun _⊑_ : ICHD3Code × ICHD3Code → 𝔹           -- h ⊑ t: h is t or a subtype of t in the ICHD-3 code hierarchy
const c1, c1_2, c1_3, c2, c2_3, c3_1, c8_2, c8_2_1, c8_2_2, c8_2_3, c8_2_4, c8_2_5, c8_2_6, c8_2_7, c8_2_8 : ICHD3Code
axiom table SD-IC
axiom ∀ h, k, t : ICHD3Code • h ⊑ h ∧ (h ⊑ k ∧ k ⊑ h ⇒ h = k) ∧ (h ⊑ k ∧ k ⊑ t ⇒ h ⊑ t)
axiom c1_2 ⊑ c1 ∧ c1_3 ⊑ c1 ∧ c2_3 ⊑ c2 ∧ c8_2_1 ⊑ c8_2 ∧ c8_2_2 ⊑ c8_2 ∧ c8_2_3 ⊑ c8_2 ∧ c8_2_4 ⊑ c8_2 ∧
  c8_2_5 ⊑ c8_2 ∧ c8_2_6 ⊑ c8_2 ∧ c8_2_7 ⊑ c8_2 ∧ c8_2_8 ⊑ c8_2
```
- Meaning: References to ICHD-3 diagnoses by code, with the code labels exactly as ICHD-3 prints them. Headache types of the subject are ICHD-3 codes. `⊑` is the code hierarchy (reflexive and transitive). "The subject has migraine" is `hasType(c, c1)`, "migraine with aura" `hasType(c, c1_2)`, "cluster headache" `hasType(c, c3_1)`, "tension-type headache" `hasType(c, c2)`. Since the headache types of a context are those of the subject's history up to the as-of date (E-008), "has" in these readings means "has or has had", and "has or may have" (`mayHaveType`) means "has or may have, or has had or may have had".
- Conformance: Structural (code labels: table SD-IC).
- Realises: OUT-005, OUT-012, OUT-013, OUT-014, OUT-016, OUT-028, OUT-029, OUT-031, OUT-037
- Evidence: Stage 1 OUT-014, OUT-016, OUT-028 (codes named). Code labels not quoted in Stage 1: [S-001] E-009/Q01, [S-001] E-009/Q02, [S-001] E-009/Q03.
- Notes: Rationale: E-009/D01.

### 5.2 Labels, caveats and per-period values

### E-010 Annotation
- Definition:
```omn
element Annotation extends Item {
  kind : AnnotationKind  core
  qualifies : set1 →Element  core  shown     -- the view or the items of the same view that the annotation qualifies
  wording : opt Text  MAY             -- the wording shown, in the language of the output
}
enum AnnotationKind ::=
    reviewPromptPossibleMedicationOveruse      -- a prompt for clinical review of possible medication overuse (OUT-016)
  | patientReportedDiaryInformation            -- the content summarises patient-reported diary information (OUT-038)
  | supportsDoesNotReplaceClinicalAssessment   -- it supports but does not replace clinical assessment and diagnosis (OUT-038)
  | requiresClinicalInterpretation             -- the indicator, label or association requires clinical interpretation (OUT-038)
  | durationInfluencedByAcuteTreatment         -- duration measures of acutely treated attacks are influenced by acute treatment (OUT-011)
  | expectedTransientWorseningEarlyWithdrawal  -- a transient worsening is expected in the early withdrawal phase (OUT-017)
  | coOccurrenceNotCausation                   -- the view shows co-occurrence and not causation (OUT-032)
  | apparentTriggersMayBePremonitorySymptoms   -- some apparent triggers are early (premonitory) symptoms of the attack (OUT-032)
  | exploratoryMeasure                         -- the measure is exploratory (OUT-008, OUT-037)
  | supportiveInformation                      -- the output is supportive information (OUT-036 Caveat)
pred annotated(e : Element, k : AnnotationKind) ≙ ∃ a : Annotation • a.kind = k ∧ e ∈ a.qualifies
```
- Meaning: A label, caption or caveat shown with the element it qualifies. `kind` fixes the substance of what is said; `wording` is the text actually shown.
- Conformance: Structural; each kind is asked for by the case of table C3 that names it (INV-120). Placement: `qualifies` (W2, definitional).
- Realises: OUT-008, OUT-011, OUT-016, OUT-017, OUT-032, OUT-036, OUT-037, OUT-038
- Evidence: Stage 1 statements of the requirements listed; OUT-036 Caveats.
- Notes: Relations: W2 (`qualifies`).

### E-011 DefinitionLabel
- Definition:
```omn
element DefinitionLabel extends Item {
  measure : LabelledMeasure  core
  definition : PublishedDefinition  core
}
enum LabelledMeasure ::= headacheDaysMeasure | migraineDaysMeasure | moderateSevereHeadacheDaysMeasure | attacksMeasure
given PublishedDefinition       -- a published definition of a measure, identified by publication and section
const ichd3HeadacheDays, ichd3FrequencyOfAttacks : PublishedDefinition   -- ICHD-3 "Definitions of terms": Headache days; Frequency of attacks
const ihs2025MigraineDay : PublishedDefinition   -- IHS position statement 2025 [S-010]: the definitions of a migraine day that its panel adopts
pred isMeasure(m : PeriodValue, lm : LabelledMeasure) ≙
  (lm = headacheDaysMeasure ∧ m ∈ HeadacheDays) ∨ (lm = migraineDaysMeasure ∧ m ∈ MigraineDays) ∨
  (lm = moderateSevereHeadacheDaysMeasure ∧ m ∈ ModerateSevereHeadacheDays) ∨ (lm = attacksMeasure ∧ m ∈ AttackCount)
pred labelledAs(v : View, lm : LabelledMeasure, d : PublishedDefinition) ≙
  (∃ l ∈ v.content ∩ DefinitionLabel • l.measure = lm) ∧ ∀ l ∈ v.content ∩ DefinitionLabel • l.measure = lm ⇒ l.definition = d
-- referencedValues(x): the per-period values that a change, a residual burden or a composite index refers to and shows
fun referencedValues(x : Item) : set PeriodValue ≙
  {ch ∈ {x} ∩ Change • ch.reference} ∪ {ch ∈ {x} ∩ Change • ch.compared} ∪
  {rb ∈ {x} ∩ ResidualBurden • rb.migraineDays} ∪ {rb ∈ {x} ∩ ResidualBurden • rb.moderateSevereHeadacheDays} ∪
  {m ∈ PeriodValue | ∃ ci ∈ {x} ∩ CompositeIndex • m ∈ ci.components}
-- reports(v, lm): the view reports the measure lm, in any form the model shows it
pred reports(v : View, lm : LabelledMeasure) ≙
  (∃ m ∈ v.content ∩ PeriodValue • isMeasure(m, lm)) ∨ (∃ x ∈ v.content; m ∈ referencedValues(x) • isMeasure(m, lm)) ∨
  (lm = headacheDaysMeasure ∧ ∃ i ∈ v.content ∩ IntensitySummary • i.summary is peakIntensityDistribution) ∨
  (lm = migraineDaysMeasure ∧ v.content ∩ MigraineFreePeriodMark ≠ ∅) ∨
  (lm ∈ {migraineDaysMeasure, attacksMeasure} ∧ v.content ∩ CycleLine ≠ ∅) ∨
  (lm = attacksMeasure ∧ (v.content ∩ ClusterAttackRate ≠ ∅ ∨ v ∈ TriggerCooccurrenceView))
fun fixedDefinition : LabelledMeasure ⇸ PublishedDefinition   -- the definition that Stage 1 fixes for the measure (INV-125)
fun fixedDefinitionLevel : LabelledMeasure ⇸ Level             -- the level at which Stage 1 fixes it
axiom table SD-DF
```
- Meaning: States which published definition a view follows for headache days, migraine days, moderate/severe headache days or attacks, for example ICHD-3 "Definitions of terms" [S-001], the IHS trial guidelines [S-002][S-003] or the 2026 eDelphi consensus definition of a migraine day [S-043]. A view follows one published definition for each of these measures: every value of the measure that the view shows, or that a change, a residual burden or a composite index shown in it refers to, follows that definition, and every definition label that the view shows for the measure names it (INV-111). `labelledAs(v, lm, d)` holds when the view states a definition for the measure lm and every definition it states for lm is d; by INV-111, a view that states a definition for lm states only one. `referencedValues(x)` is the set of per-period values that an item refers to and shows as part of itself: the two values a change compares (E-040), the two day counts of a residual burden (E-044) and the component measures of a composite index (E-033). `reports(v, lm)` holds when the view reports the measure lm in any form the model shows it: a per-period value of the measure (`isMeasure`), shown in the view or referred to by a change, a residual burden or a composite index shown in it; for headache days, a distribution of headache days by peak intensity (E-023); for migraine days, the mark of a period without migraine days (E-022); for migraine days and attacks, a cycle line, which shows the migraine days and the migraine attacks of a menstrual cycle (E-060, E-061); and for attacks, a cluster attack rate (E-064) or a trigger co-occurrence view, which shows the onsets of attacks (E-065).
- Conformance: Availability: SHOULD, for each measure that a view reports (`reports`; INV-008). Definitional: INV-111. Fixed definitions: INV-125 (SD-DF-01 MUST, SD-DF-02 SHOULD).
- Realises: OUT-002, OUT-004, OUT-005, OUT-006, OUT-007, OUT-028
- Evidence: Stage 1 OUT-002, OUT-004, OUT-005, OUT-006, OUT-007, OUT-028. The definitions of a migraine day of the IHS position statement 2025 (`ihs2025MigraineDay`) are not named in Stage 1; [S-010] quoted in E-018.
- Notes: `PublishedDefinition` is a given set because Stage 1 names examples, not a closed list. Rationale: E-011/D01, E-011/D02.

### E-012 PeriodValue
- Definition:
```omn
abstract element PeriodValue extends Item {
  period : →Period  core          -- the reporting period the value refers to
  typeScope : TypeScope  core     -- all headache types combined, or one headache type
}
variant TypeScope ::= allTypes | ofType ⟨HeadacheType⟩
pred concerns(c : OutputContext, sc : TypeScope, t : ICHD3Code) ≙
  (∃ h : HeadacheType • sc = ofType(h) ∧ h ⊑ t) ∨
  (sc = allTypes ∧ c.subject.headacheTypes ≠ ∅ ∧ ∀ h ∈ c.subject.headacheTypes • h ⊑ t)
pred onlyOfType(c : OutputContext, sc : TypeScope, t : ICHD3Code) ≙
  concerns(c, sc, t) ∧ (sc = allTypes ⇒ ∀ h ∈ c.subject.possibleHeadacheTypes • h ⊑ t)
pred scopeFor(c : OutputContext, sc : TypeScope, t : ICHD3Code) ≙
  (onlyOfType(c, allTypes, t) ∧ sc = allTypes) ∨ (¬ onlyOfType(c, allTypes, t) ∧ sc = ofType(t))
-- daysWithin(x): the numbers of days within its period that the value x shows (INV-121)
fun daysWithin(x : PeriodValue) : set ℕ ≙
  {m ∈ {x} ∩ DayCount • m.days} ∪
  {n : ℕ | ∃ ci ∈ {x} ∩ CompletenessIndicator • coveredDays(n) ∈ ci.expressions} ∪
  {n : ℕ | ∃ i ∈ {x} ∩ IntensitySummary; ds : set1 LevelDays • i.summary = peakIntensityDistribution(ds) ∧ ∃ ld ∈ ds • ld.days = n} ∪
  {n : ℕ | ∃ a ∈ {x} ∩ AssociatedSymptomSummary • a.presence = daysWithSymptom(n)} ∪
  {n : ℕ | ∃ ci ∈ {x} ∩ CaregiverImpact • ci.impact = caregiverLostProductiveDays(n)}
```
- Meaning: A value shown for one reporting period. `typeScope` is `allTypes` for values over all headache types combined and `ofType(t)` for the separate presentation per headache type of OUT-029. `concerns(c, sc, t)` holds when a value with scope sc concerns headache type t: it is scoped to t or a subtype, or it covers all types of a subject who has a headache type and whose headache types all fall under t (used for "for migraine" and "for tension-type headache" in OUT-037). `onlyOfType(c, sc, t)` holds when the values with scope sc are values of headache type t only: they concern t, and, if they cover all headache types, every headache type the subject has or may have falls under t. `scopeFor(c, sc, t)` holds when sc is the scope of the values of all the subject's headaches of type t: all headache types combined where the subject has a headache type and every headache type it has or may have falls under t, and the scope of t itself (`ofType(t)`) otherwise; exactly one scope satisfies it.
- Conformance: Structural. Definitional: INV-121, INV-122.
- Realises: OUT-001, OUT-020, OUT-023, OUT-029, OUT-031, OUT-037
- Evidence: Stage 1 OUT-001, OUT-029 ("When the patient has, or may have, more than one headache type"); OUT-020, OUT-023 and OUT-031 for the relations that use `onlyOfType` and `scopeFor` (E-045, E-046, E-064, INV-062, INV-073, INV-088, INV-089).
- Notes: Relations: INV-003. Rationale: E-012/D01.

### E-013 CompletenessIndicator
- Definition:
```omn
element CompletenessIndicator extends PeriodValue {
  expressions : set1 CompletenessExpression  derived core    -- how completely the period is covered, in one or more forms
}
variant CompletenessExpression ::= coveredDays ⟨ℕ⟩           -- days of the period covered by diary information; unit: days
  | proportionCovered ⟨Percent⟩                              -- proportion of the period's days covered by diary information; unit: %
  | otherCompletenessExpression ⟨Text⟩                       -- another expression of how completely the period is covered, as worded
```
- Meaning: How completely a reporting period is covered by diary information, shown next to the summary measures of that period so that readers can judge their reliability.
- Conformance: Availability: SHOULD (INV-011). Definitional: INV-012, INV-121. Prohibited: C2-02.
- Realises: OUT-003
- Evidence: Stage 1 OUT-003.
- Notes: Relations: INV-012, INV-121. Rationale: E-013/D01, E-013/D02, E-013/N01.

### E-014 DayCount
- Definition:
```omn
element DayCount extends PeriodValue {
  measure : DayMeasure  core
  days : ℕ  derived core          -- number of days of the period with the property; unit: days
}
variant DayMeasure ::= headacheDays | migraineDays | moderateSevereHeadacheDays
  | migraineOrModerateSevereHeadacheDays | headacheFreeDays | symptomFreeDays
  | acuteMedicationDays ⟨MedicationScope⟩
  | functionalImpactDays ⟨ImpactDomain × ImpactSeverity⟩
pred dayCount(v : View, k : DayMeasure, p : Period, sc : TypeScope, n : ℕ) ≙
  ∃ m ∈ v.content ∩ DayCount • m.measure = k ∧ m.period = p ∧ m.typeScope = sc ∧ m.days = n
pred shownDay(v : View, k : DayMeasure, p : Period, sc : TypeScope) ≙ ∃ n : ℕ • dayCount(v, k, p, sc, n)
fun daysOf(v : View, k : DayMeasure, p : Period, sc : TypeScope) : set ℕ ≙
  {m ∈ v.content ∩ DayCount | m.measure = k ∧ sameSpan(m.period, spanOf(p)) ∧ m.typeScope = sc • m.days}   -- at most one member (INV-006)
-- nestedIn(k₁, k₂): every day with the property of k₁ has the property of k₂ (INV-122)
pred nestedIn(k₁ : DayMeasure, k₂ : DayMeasure) ≙
  (k₁ = moderateSevereHeadacheDays ∧ k₂ = headacheDays) ∨
  (k₁ = symptomFreeDays ∧ k₂ = headacheFreeDays) ∨
  (∃ k : AcuteDrugClass • k₁ = acuteMedicationDays(ofClass(k)) ∧ k₂ = acuteMedicationDays(allAcuteMedication)) ∨
  (∃ dr ∈ dom classOf • k₁ = acuteMedicationDays(ofDrug(dr)) ∧ k₂ = acuteMedicationDays(ofClass(classOf(dr)))) ∨
  (∃ ks : set1 AcuteDrugClass; k ∈ ks • k₁ = acuteMedicationDays(ofClass(k)) ∧ k₂ = acuteMedicationDays(ofClasses(ks))) ∨
  (∃ ks : set1 AcuteDrugClass • k₁ = acuteMedicationDays(ofClasses(ks)) ∧ k₂ = acuteMedicationDays(allAcuteMedication)) ∨
  (∃ d : ImpactDomain; s ∈ {missed, impaired, severelyImpaired} • k₁ = functionalImpactDays((d, s)) ∧ k₂ = functionalImpactDays((d, affected)))
```
- Meaning: A number of days within a reporting period, of one kind. The kinds are specified in E-015 to E-018, E-020, E-021, E-029 and E-030. `dayCount(v, k, p, sc, n)` holds when the view v shows a count of kind k and type scope sc for the period atom p, with n days, and `shownDay(v, k, p, sc)` when it shows such a count with any number of days. `daysOf(v, k, p, sc)` is the set of the numbers of days that v shows for kind k and type scope sc for a period with the dates of p, whichever period atom each count refers to; it has at most one member (INV-006). The relations among per-period values use `daysOf`, so they hold for a reporting period as its start and end dates identify it to the reader.
- Conformance: Structural; each kind has its own conformance. Definitional: INV-006, INV-121, INV-122.
- Realises: OUT-004, OUT-005, OUT-006, OUT-008, OUT-014, OUT-020, OUT-027
- Evidence: Stage 1 statements of the requirements listed.
- Notes: Relations: INV-006, INV-024, INV-031, INV-121, INV-122. Rationale: E-014/D01.

### E-015 HeadacheDays
- Definition:
```omn
type HeadacheDays == {m : DayCount | m.measure = headacheDays}
```
- Meaning: The number of headache days in the reporting period, with "headache days" as defined in ICHD-3 "Definitions of terms" [S-001].
- Conformance: Availability: MUST (INV-118, C1-01). Definition label: SHOULD (INV-008); fixed definition MUST (INV-125, SD-DF-01).
- Realises: OUT-001, OUT-002, OUT-004
- Evidence: Stage 1 OUT-001, OUT-002, OUT-004.

### E-016 MigraineDays
- Definition:
```omn
type MigraineDays == {m : DayCount | m.measure = migraineDays}
```
- Meaning: The number of migraine days in the reporting period (monthly migraine days for calendar months or 28-day periods), under the one published definition that the view follows for migraine days, which its definition labels name (E-011, INV-111).
- Conformance: Availability: MUST (INV-118, C1-02); applicability: "For patients with migraine", `hasType(c, c1)`. Definition label: SHOULD (INV-008).
- Realises: OUT-001, OUT-002, OUT-005
- Evidence: Stage 1 OUT-001, OUT-002, OUT-005.
- Notes: Relations: INV-031. Rationale: E-016/D01.

### E-017 ModerateSevereHeadacheDays
- Definition:
```omn
type ModerateSevereHeadacheDays == {m : DayCount | m.measure = moderateSevereHeadacheDays}
```
- Meaning: The number of days in the reporting period with headache of moderate or severe intensity, under the one published definition that the view follows for these days, which its definition labels name (E-011, INV-111).
- Conformance: Availability: SHOULD (INV-118, C1-03); MUST where provided (INV-118, C1-04). Definition label: SHOULD (INV-008). Definitional: INV-122.
- Realises: OUT-001, OUT-002, OUT-006
- Evidence: Stage 1 OUT-001, OUT-002, OUT-006.

### E-018 MigraineOrModerateSevereHeadacheDays
- Definition:
```omn
type MigraineOrModerateSevereHeadacheDays == {m : DayCount | m.measure = migraineOrModerateSevereHeadacheDays}
```
- Meaning: The number of days in the reporting period with migraine or moderate-to-severe headache, the single count on which the control levels of the IHS position statement 2025 rest, with migraine days as that statement defines them: under the definitions of a migraine day that its panel adopts for the assessment of its control levels (`ihs2025MigraineDay`, E-011).
- Conformance: Availability: none of its own. Content: SHOULD with a control-level label (INV-062). Definitional: INV-031.
- Realises: OUT-020
- Evidence: Stage 1 OUT-020 (the named criterion "IHS position statement 2025 control levels" and the requirement to show the values it rests on). The count on which the control levels rest, and the definition of a migraine day it follows: [S-010] E-018/Q01, [S-010] E-018/Q02, [S-010] E-018/Q03.
- Notes: Relations: INV-031. See ISS-05. Rationale: E-018/D01, E-018/D02.

### E-019 EventCount and AttackCount
- Definition:
```omn
element EventCount extends PeriodValue {
  event : CountedEvent  core
  count : ℕ  derived core         -- number of events in the period; unit: attacks or auras
}
enum CountedEvent ::= attacks | auras
type AttackCount == {m : EventCount | m.event = attacks}
```
- Meaning: The number of attacks or of auras (E-027) in the reporting period, shown as a value of its own, separately from headache or migraine days. Attacks are counted under the one published definition that the view follows for attacks, which its definition labels name (E-011, INV-111); INV-125 (SD-DF-02) asks, at SHOULD, that the label name the frequency of attacks as defined in ICHD-3 "Definitions of terms" [S-001].
- Conformance: Availability: attacks SHOULD (INV-118, C1-05); MUST where provided (INV-118, C1-06); aura counts MAY (E-027). Definition label: SHOULD (INV-008); fixed definition SHOULD (INV-125, SD-DF-02). Definitional: INV-006, INV-122.
- Realises: OUT-001, OUT-002, OUT-007, OUT-013
- Evidence: Stage 1 OUT-001, OUT-002, OUT-007, OUT-013.
- Notes: Relations: INV-006, INV-033, INV-089, INV-122. Rationale: E-019/D01.

### E-020 HeadacheFreeDays
- Definition:
```omn
type HeadacheFreeDays == {m : DayCount | m.measure = headacheFreeDays}
```
- Meaning: The number of headache-free days in the reporting period, an exploratory measure of residual burden.
- Conformance: Availability: MAY; SHOULD in the clinician-facing summary (INV-104; see ISS-04). Labels and caveats: C3-02 (MAY). Definitional: INV-031.
- Realises: OUT-008
- Evidence: Stage 1 OUT-008.
- Notes: Relations: INV-031. See ISS-04. Rationale: E-020/D01.

### E-021 SymptomFreeDays
- Definition:
```omn
type SymptomFreeDays == {m : DayCount | m.measure = symptomFreeDays}
```
- Meaning: The number of symptom-free days in the reporting period (days free of premonitory, aura, headache and postdromal symptoms, as quoted in Stage 1 OUT-008 from [S-002]), an exploratory measure of residual burden.
- Conformance: Availability: MAY; SHOULD in the clinician-facing summary (INV-104; see ISS-04). Labels and caveats: C3-02 (MAY). Definitional: INV-122.
- Realises: OUT-008
- Evidence: Stage 1 OUT-008.
- Notes: Relations: INV-122. See ISS-04.

### E-022 MigraineFreePeriodMark
- Definition:
```omn
element MigraineFreePeriodMark extends PeriodValue { }
```
- Meaning: Marks a reporting period without migraine days ("periods without migraine days", migraine freedom), an exploratory measure of residual burden.
- Conformance: Availability: MAY; SHOULD in the clinician-facing summary (INV-104; see ISS-04). Labels and caveats: C3-02 (MAY). Definitional: INV-031. Definition label: SHOULD (INV-008, `reports`).
- Realises: OUT-008
- Evidence: Stage 1 OUT-008.
- Notes: Relations: INV-031. See ISS-03, ISS-04. Rationale: E-022/D01.

### E-023 IntensitySummary
- Definition:
```omn
element IntensitySummary extends PeriodValue {
  scale : opt IntensityScale  SHOULD          -- the scale on which intensity is shown
  summary : IntensitySummaryValue  derived core
}
value IntensityScale { name : Text; points : seq1 ScalePoint }
value ScalePoint { score : ℚ; label : opt Text }       -- a point of the scale, with its verbal label if the scale has one
variant IntensitySummaryValue ::=
    peakIntensityDistribution ⟨set1 LevelDays⟩       -- headache days by peak intensity level
  | meanPeakIntensity ⟨ℚ⟩                            -- average peak intensity on the scale; unit: scale points
  | otherIntensitySummary ⟨OtherSummary⟩             -- a summary in another form, which states that form
value LevelDays { level : ScalePoint; days : ℕ }      -- unit: days
value OtherSummary { form : Text; value : Text }      -- form: the kind of summary as the output names it, for example median
                                                      --   peak intensity; value: the value as the output words it
-- onSameScale(i₁, i₂): the two summaries state intensity on the same scale and in the same form (both distributions of headache
-- days by peak intensity, both mean peak intensities, or both of the same other form)
pred onSameScale(i₁ : IntensitySummary, i₂ : IntensitySummary) ≙ i₁.scale = i₂.scale ∧
  (i₁.summary is peakIntensityDistribution ⇔ i₂.summary is peakIntensityDistribution) ∧
  (i₁.summary is meanPeakIntensity ⇔ i₂.summary is meanPeakIntensity) ∧
  (∀ x₁, x₂ : OtherSummary • i₁.summary = otherIntensitySummary(x₁) ∧ i₂.summary = otherIntensitySummary(x₂) ⇒ x₁.form = x₂.form)
```
- Meaning: A summary of headache intensity in the reporting period on a stated scale, for example the distribution of headache days by peak intensity category or an average peak intensity. A summary in another form states that form, as the output names it, with its value (`OtherSummary`). `onSameScale(i₁, i₂)` holds when two summaries state intensity on the same scale and in the same form: both distributions of headache days by peak intensity, both mean peak intensities, or both of the same other form.
- Conformance: Availability: SHOULD (INV-118, C1-07); between periods SHOULD (INV-039); per headache type SHOULD where provided (INV-118, C1-14). Content: INV-069, INV-105 (SHOULD). Definitional: INV-032, INV-121. Definition label: SHOULD (INV-008, `reports`).
- Realises: OUT-010, OUT-021, OUT-029, OUT-035
- Evidence: Stage 1 OUT-010, OUT-021, OUT-035; [S-030] E-023/Q00.
- Notes: Relations: INV-032, INV-121. Rationale: E-023/D01, E-023/D02.

### E-024 DurationSummary
- Definition:
```omn
element DurationSummary extends PeriodValue {
  kind : DurationKind  core
  statistic : SummaryStatistic  core
  value : Duration  derived core
  attackScope : AttackScope  core          -- which attacks the summary covers
}
enum DurationKind ::= attackDuration | headacheDuration | moderateSeverePainTime | auraDuration
enum SummaryStatistic ::= median | mean | total | otherStatistic
enum AttackScope ::= allAttacks | acutelyTreatedAttacks | untreatedAttacks
```
- Meaning: A summary of attack or headache duration in the reporting period, for example the median attack duration or the hours with moderate/severe pain per 28 days (`moderateSeverePainTime` with statistic `total` over a 28-day period). `auraDuration` is the aura duration of OUT-013.
- Conformance: Availability: SHOULD (INV-118, C1-08). Definitional: INV-121. Labels and caveats: C3-03. Prohibited: C2-03.
- Realises: OUT-011, OUT-013
- Evidence: Stage 1 OUT-011, OUT-013.
- Notes: Relations: INV-121.

### E-025 AssociatedSymptomSummary
- Definition:
```omn
element AssociatedSymptomSummary extends PeriodValue {
  symptom : AssociatedSymptom  core
  presence : SymptomPresence  derived core
}
enum AssociatedSymptom ::= nauseaOrVomiting | photophobia | phonophobia
variant SymptomPresence ::= daysWithSymptom ⟨ℕ⟩ | attacksWithSymptom ⟨ℕ⟩ | otherPresenceSummary ⟨OtherSummary⟩   -- OtherSummary: E-023
-- inSameForm(a₁, a₂): the two summaries state presence in the same form and unit (both as days with the symptom, both as attacks
-- with the symptom, or both in the same other form)
pred inSameForm(a₁ : AssociatedSymptomSummary, a₂ : AssociatedSymptomSummary) ≙
  (a₁.presence is daysWithSymptom ⇔ a₂.presence is daysWithSymptom) ∧
  (a₁.presence is attacksWithSymptom ⇔ a₂.presence is attacksWithSymptom) ∧
  (∀ x₁, x₂ : OtherSummary • a₁.presence = otherPresenceSummary(x₁) ∧ a₂.presence = otherPresenceSummary(x₂) ⇒ x₁.form = x₂.form)
```
- Meaning: The presence of a migraine-associated symptom (nausea/vomiting, photophobia, phonophobia) in the reporting period. A summary in another form states that form, as the output names it, with its value (`OtherSummary`, E-023). `inSameForm(a₁, a₂)` holds when two summaries state presence in the same form and unit: both as days with the symptom, both as attacks with the symptom, or both in the same other form.
- Conformance: Availability: SHOULD (INV-118, C1-09); applicability: "For migraine", `hasType(c, c1)`. Content: INV-069 (SHOULD). Definitional: INV-033, INV-121.
- Realises: OUT-012, OUT-021
- Evidence: Stage 1 OUT-012; for one form in the treatment review view, OUT-021 ("The purpose is that efficacy can be judged across these dimensions").
- Notes: Relations: INV-033, INV-121. Rationale: E-025/D01.

### E-026 MostBothersomeSymptomItem
- Definition:
```omn
element MostBothersomeSymptomItem extends PeriodValue {
  symptom : Symptom  core
}
variant Symptom ::= associated ⟨AssociatedSymptom⟩ | otherNonPainSymptom ⟨Text⟩
```
- Meaning: The patient's most bothersome symptom, shown for a reporting period. Its absence at the early time point after treatment is an outcome of E-050.
- Conformance: Availability: SHOULD (INV-118, C1-09); applicability: "For migraine", `hasType(c, c1)`. Content: INV-069 (SHOULD).
- Realises: OUT-012, OUT-021
- Evidence: Stage 1 OUT-012.

### E-027 Aura measures
- Definition:
```omn
type AuraCount == {m : EventCount | m.event = auras}
type AuraDuration == {m : DurationSummary | m.kind = auraDuration}
```
- Meaning: The number of auras in the reporting period and their duration, shown separately from headache measures.
- Conformance: Availability: MAY; applicability: "patients with migraine with aura", `hasType(c, c1_2)`.
- Realises: OUT-013
- Evidence: Stage 1 OUT-013.
- Notes: See ISS-04. Rationale: E-027/D01.

### E-028 AcuteDrugClass
- Definition:
```omn
enum AcuteDrugClass ::= ergotamine | triptans | nonOpioidAnalgesics | opioids | combinationAnalgesics | otherMedication
fun classCode : AcuteDrugClass → ICHD3Code
axiom table SD-CLS
fun classOf : Drug ⇸ AcuteDrugClass      -- the ICHD-3 8.2 class of an acute medication
const classesOf826 : set1 AcuteDrugClass ≙ {ergotamine, triptans, nonOpioidAnalgesics, opioids}
const classesOf821to825 : set1 AcuteDrugClass ≙ {ergotamine, triptans, nonOpioidAnalgesics, opioids, combinationAnalgesics}
```
- Meaning: The classes of acute (symptomatic) headache medication as used in ICHD-3 code 8.2 and its subtypes. Each class is shown with the label of its ICHD-3 subtype (`label(classCode(k))`). `classOf` assigns each acute medication to its class. `classesOf826` are the classes whose combined use ICHD-3 8.2.6 refers to.
- Conformance: Structural (codes and reference levels: table SD-CLS).
- Realises: OUT-014, OUT-016
- Evidence: Stage 1 OUT-014, OUT-016. Details not stated in Stage 1: [S-001] E-009/Q03, [S-001] E-028/Q01, [S-001] E-028/Q02, [S-001] E-028/Q03.
- Notes: See ISS-01, ISS-02. Rationale: E-028/D01.

### E-029 AcuteMedicationDays
- Definition:
```omn
variant MedicationScope ::= allAcuteMedication | ofClass ⟨AcuteDrugClass⟩ | ofDrug ⟨Drug⟩ | ofClasses ⟨set1 AcuteDrugClass⟩
type AcuteMedicationDays == {m : DayCount | ∃ s : MedicationScope • m.measure = acuteMedicationDays(s)}
type TotalAcuteMedicationDays == {m : DayCount | m.measure = acuteMedicationDays(allAcuteMedication)}
-- medicationKinds(c): the kinds of acute-medication day counts asked for per period (table C1, rows C1-10 and C1-13)
fun medicationKinds(c : OutputContext) : set (ℙ PeriodValue) ≙ {TotalAcuteMedicationDays} ∪
  {m ∈ c.subject.acuteMedications • {d : DayCount | d.measure = acuteMedicationDays(ofClass(classOf(m.drug)))}} ∪
  {m ∈ c.subject.acuteMedications • {d : DayCount | d.measure = acuteMedicationDays(ofDrug(m.drug))}}
```
- Meaning: The number of days in the reporting period with acute (symptomatic) headache medication: in total across classes (`allAcuteMedication`), per ICHD-3 8.2 class (`ofClass`), per individual drug (`ofDrug`), and, as the basis of the 8.2.6 indicator, for any medication of a set of classes (`ofClasses(classesOf826)`).
- Conformance: Availability: MUST (INV-118, C1-10); per calendar week SHOULD (INV-118, C1-11); per headache type MUST (INV-118, C1-13). Definitional: INV-024, INV-045, INV-122, INV-123 (`usedScope`).
- Realises: OUT-014, OUT-015, OUT-016, OUT-029
- Evidence: Stage 1 OUT-014, OUT-015, OUT-016, OUT-029; [S-001] 8.2.6 criterion B quoted in E-028.
- Notes: Relations: INV-024, INV-122, INV-123. A day with two classes counts once in the total and once in each class, so the total is in general not the sum. See ISS-01, ISS-09. Rationale: E-029/D01.

### E-030 FunctionalImpactDays
- Definition:
```omn
enum ImpactDomain ::= paidWorkOrSchool | householdWork | socialOrLeisure | anyActivity
enum ImpactSeverity ::= affected | missed | impaired | severelyImpaired
type FunctionalImpactDays == {m : DayCount | ∃ d : ImpactDomain; s : ImpactSeverity • m.measure = functionalImpactDays((d, s))}
fun fiDays(d : ImpactDomain, s : ImpactSeverity) : ℙ DayCount ≙ {m : DayCount | m.measure = functionalImpactDays((d, s))}
```
- Meaning: The number of days in the reporting period on which headache affected paid work or school, household work, or social or leisure activities (`affected`), including days with severe functional impairment (`severelyImpaired`), in days per period. For children, school days missed (`missed`) or impaired (`impaired`) in the domain `paidWorkOrSchool`. `anyActivity` is used for days with severe impairment of any activity.
- Conformance: Availability: SHOULD (INV-118, C1-12); comparison with the baseline period SHOULD (INV-027); school days SHOULD for children and adolescents (INV-096). Definitional: INV-121, INV-122.
- Realises: OUT-027, OUT-036
- Evidence: Stage 1 OUT-027, OUT-036.
- Notes: Relations: INV-121, INV-122.

### E-031 CaregiverImpact
- Definition:
```omn
element CaregiverImpact extends PeriodValue {
  impact : CaregiverImpactValue  derived core
}
variant CaregiverImpactValue ::= caregiverLostProductiveDays ⟨ℕ⟩ | otherCaregiverImpact ⟨Text⟩    -- unit of the first: days
```
- Meaning: The impact of a child's or adolescent's headache on parents or caregivers in the reporting period, for example their lost productive time in days.
- Conformance: Availability: SHOULD for children and adolescents (INV-096). Definitional: INV-121.
- Realises: OUT-036
- Evidence: Stage 1 OUT-036.
- Notes: Relations: INV-121.

### E-032 MedicationOveruseIndicator
- Definition:
```omn
element MedicationOveruseIndicator extends Item {
  period : →Period  core                  -- the reporting period the indication is given for (a calendar month or 28-day period)
  scope : OveruseScope  core
  code : ICHD3Code  derived MUST          -- the ICHD-3 subtype the indication refers to, shown with its label
  referenceLevel : ℕ₁  derived MUST       -- the level of regular use of that subtype; unit: days per month
  span : seq1 →Period  MUST               -- the consecutive monthly periods of the time span the code refers to
  basis : seq1 →DayCount  MUST            -- the acute-medication days of the scope, one for each period of the span
  status : OveruseStatus  derived core
}
variant OveruseScope ::= ofClassUse ⟨AcuteDrugClass⟩ | combinedUse
enum OveruseStatus ::= levelReached | levelNotReached
fun overuseCode : OveruseScope → ICHD3Code
fun overuseLevel : OveruseScope → ℕ₁
fun basisScope : OveruseScope → MedicationScope
axiom ∀ k : AcuteDrugClass • overuseCode(ofClassUse(k)) = classCode(k) ∧ basisScope(ofClassUse(k)) = ofClass(k)
axiom table SD-CMB                         -- combined use; overuseLevel(ofClassUse(k)): table SD-CLS (axiom in E-028)
-- sameIndicatedPeriod(i₂, i): i₂ is shown in the view of i for a period with the dates and the kind of the period of i
pred sameIndicatedPeriod(i₂ : MedicationOveruseIndicator, i : MedicationOveruseIndicator) ≙
  i₂ ∈ viewOf(i).content ∧ sameSpan(i₂.period, spanOf(i.period)) ∧ i₂.period.kind = i.period.kind
-- classShownUsed(i, k, j): an indicator of class k for the same period as i shows days with class k in the j-th period of its span
pred classShownUsed(i : MedicationOveruseIndicator, k : AcuteDrugClass, j : ℕ₁) ≙
  ∃ i₂ : MedicationOveruseIndicator • sameIndicatedPeriod(i₂, i) ∧ i₂.scope = ofClassUse(k) ∧ j ∈ dom i₂.basis ∧ i₂.basis(j).days > 0
-- classUseExcluded(i, k): no indicator of class k for the same period as i shows days with class k in its span, and either the
-- subject has used no medication of class k up to the as-of date or such an indicator is shown (and then shows 0 days in
-- every period of its span)
pred classUseExcluded(i : MedicationOveruseIndicator, k : AcuteDrugClass) ≙
  (¬ ∃ j ∈ dom i.basis • classShownUsed(i, k, j)) ∧
  ((¬ ∃ m ∈ ctx(outputOf(i)).subject.acuteMedications • classOf(m.drug) = k) ∨
   (∃ i₂ : MedicationOveruseIndicator • sameIndicatedPeriod(i₂, i) ∧ i₂.scope = ofClassUse(k)))
```
- Meaning: For one reporting period and one acute-medication class, or for the combined use of the classes of ICHD-3 8.2.6, whether acute medication use reached the level of regular use that the ICHD-3 subtype describes over the time span that subtype refers to. The output shows the subtype, its reference level (10 or 15 days per month) and the time span (more than 3 months) next to the indication, and it shows the medication days on which the indication rests (`basis`). It is worded as a prompt for clinical review of possible medication overuse and is not a diagnosis of medication-overuse headache.
- Conformance: Availability: MUST (INV-044). Definitional: INV-045, INV-046. Labels and caveats: C3-04 (MUST), C3-05 (SHOULD). Prohibited: C2-04 (MUST NOT).
- Realises: OUT-014, OUT-016, OUT-038
- Evidence: Stage 1 OUT-016. Reference levels and time span, not stated in Stage 1: [S-001] E-032/Q01, [S-001] E-032/Q02, [S-001] E-032/Q03, [S-001] E-032/Q04, [S-001] E-032/Q05, [S-001] E-032/Q06, [S-001] E-032/Q07, [S-001] E-028/Q02, E-028/Q03, INV-046/Q01.
- Notes: Relations: INV-045, INV-046. The indicators of the same period are those that the same view shows for a period with the same dates and the same kind (`sameIndicatedPeriod`): their spans have the same dates (INV-045), so they rest on the same days, which the view shows with one number for each period of the span (INV-006). See ISS-01, ISS-09. Rationale: E-032/D01, E-032/D02, E-032/D03, E-032/N01.

### E-033 CompositeIndex
- Definition:
```omn
element CompositeIndex extends PeriodValue {
  index : HeadacheIndexKind  core
  combines : {s : set IndexDimension | #s ≥ 2}  core     -- the dimensions the index combines into one score
  value : ℚ  derived core                               -- unit: as the index defines it
  role : MeasureRole  core                              -- how the output presents the index
  components : set →PeriodValue  SHOULD when concerns(ctx, self.typeScope, c1)  shown SHOULD when concerns(ctx, self.typeScope, c1)   -- the component measures shown with it
}
variant HeadacheIndexKind ::= areaUnderHeadacheCurve | otherHeadacheIndex ⟨Text⟩   -- another index, by the name the output shows for it
enum IndexDimension ::= frequency | intensity | duration
enum MeasureRole ::= primaryRole | secondaryRole | exploratoryRole
pred dimensionOf(m : PeriodValue, d : IndexDimension) ≙
  (d = frequency ∧ m ∈ HeadacheDays ∪ MigraineDays ∪ ModerateSevereHeadacheDays ∪ AttackCount) ∨
  (d = intensity ∧ m ∈ IntensitySummary) ∨ (d = duration ∧ m ∈ DurationSummary)
```
- Meaning: A headache index that multiplies or otherwise combines frequency, intensity and/or duration into one score, including the area under the headache curve (AUC) of the IHS tension-type headache trial guideline (section 2.3.3.2 [S-006]). `otherHeadacheIndex(x)` is another index, shown by its name x, so that two different indices are not one kind of index (`compositeIndicesOf`, E-045). `role` states whether the output presents it as a primary measure.
- Conformance: Availability: none (Stage 1 neither requires nor recommends an index). Content: INV-092, INV-093 (SHOULD). Prohibited: INV-091 (SHOULD NOT). Definitional: INV-115. Labels and caveats: C3-12. Placement: `components` (W2, SHOULD, `when concerns(ctx, self.typeScope, c1)`).
- Realises: OUT-037
- Evidence: Stage 1 OUT-037.
- Notes: Relations: INV-115. Rationale: E-033/D01.

### 5.3 Views over time and comparisons

### E-034 TreatmentMarker
- Definition:
```omn
element TreatmentMarker extends Item {
  treatment : Treatment  core
  event : {k : CourseEventKind | markedKind(k)}  core     -- start, dose change or stop (discontinued or paused)
  date : Date  core
}
pred markedKind(k : CourseEventKind) ≙ k is start ∨ k is doseChange ∨ k is stop
```
- Meaning: A dated marker in a time-course view for the start, a dose change or the stop of a preventive treatment, so that the onset of effect and the trajectory of response can be related to the treatment course.
- Conformance: Content of E-035: SHOULD (INV-035). Definitional: INV-123.
- Realises: OUT-009
- Evidence: Stage 1 OUT-009.
- Notes: Relations: INV-123.

### E-035 TimeCourseView
- Definition:
```omn
element TimeCourseView extends View {
  series : →Series  core  shown SHOULD
  markers : set →TreatmentMarker  SHOULD when ∃ e ∈ ctx.subject.courseEvents •
      e.treatment ∈ ctx.subject.preventiveTreatments ∧ markedKind(e.kind) ∧ self.covers.start ≤ e.date ∧ e.date ≤ self.covers.end  shown SHOULD
}
```
- Meaning: Frequency measures (headache days, migraine days, moderate/severe headache days, attacks) shown as a time series of consecutive reporting periods (for example a chart of consecutive months or 28-day periods, or of weeks), with dated markers for the start, dose changes and stop of preventive treatments, so that onset of effect, the trajectory of response and spontaneous fluctuation can be seen.
- Conformance: Availability: SHOULD (INV-034); weekly granularity: `ctx.weeklyGranularityRelevant`. Content: SHOULD (INV-035). Placement: `series`, `markers` (W2, SHOULD).
- Realises: OUT-009, OUT-034, OUT-035
- Evidence: Stage 1 OUT-009.

### E-036 WeeklyMedicationView
- Definition:
```omn
type WeeklyMedicationView == {v : View | ∃ sr ∈ v.content ∩ Series •
  sr.granularity = calendarWeek ∧ perPeriod(v, sr, TotalAcuteMedicationDays, allTypes)}
```
- Meaning: Acute-medication days per calendar week, in addition to the per-period totals of E-029, so that use on several days within a week is visible.
- Conformance: Availability: SHOULD (INV-118, C1-11).
- Realises: OUT-015
- Evidence: Stage 1 OUT-015.
- Notes: See ISS-09. Rationale: E-036/D01.

### E-037 PeriodComparison
- Definition:
```omn
element PeriodComparison extends Item {
  periods : {s : seq →Period | #s ≥ 2}  core     -- the compared periods, in order
  values : set1 →PeriodValue  core               -- the values shown for the compared periods
}
pred matchesSelection(pc : PeriodComparison, c : OutputContext) ≙
  #pc.periods = #c.comparedSpans ∧ ∀ i ∈ dom pc.periods • sameSpan(pc.periods(i), c.comparedSpans(i))
```
- Meaning: A side-by-side comparison of values for two or more periods, for example a pre-treatment baseline period against a later period of the same length (OUT-001), intensity between periods (OUT-010), or functional impact against the baseline period (OUT-027).
- Conformance: Availability: MUST (INV-037); intensity SHOULD (INV-039) — R-MCF (3). Content: INV-097 (SHOULD). Definitional: INV-038.
- Realises: OUT-001, OUT-010, OUT-027, OUT-036
- Evidence: Stage 1 OUT-001, OUT-010, OUT-036.
- Notes: Relations: INV-038. R-MCF (3). Rationale: E-037/D01.

### E-038 ThreeMonthPatternView
- Definition:
```omn
element ThreeMonthPatternView extends View {
  series : →Series  core  shown                -- the three most recent consecutive monthly periods
  referencedCodes : set ICHD3Code  SHOULD      -- the ICHD-3 codes the view refers to
}
pred mostRecent(sr : Series, d : Date) ≙
  last(sr.periods).end ≤ d ∧ d < periodEndFrom(sr.granularity, next(last(sr.periods).end))
```
- Meaning: Headache days and migraine days for each of the most recent three consecutive calendar months or 28-day periods, so that a clinician can relate the pattern to ICHD-3 code 1.3 Chronic migraine (and to 2.3 Chronic tension-type headache where relevant). The view does not itself assign a diagnosis.
- Conformance: Availability: MUST (INV-040). Content: SHOULD (INV-042). Definitional: INV-041. Prohibited: C2-08. Placement: `series` (W2, definitional).
- Realises: OUT-028, OUT-038
- Evidence: Stage 1 OUT-028.
- Notes: Relations: INV-041. See ISS-03. Rationale: E-038/D01.

### 5.4 Medication overuse and withdrawal

### E-039 WithdrawalFollowUpView
- Definition:
```omn
element WithdrawalFollowUpView extends View {
  withdrawalStart : Date  core
  series : opt →Series  SHOULD when wholePeriodFrom(self.withdrawalStart, self.covers)  shown SHOULD   -- consecutive whole periods from the
                                                                                                      --   start of withdrawal onward
  reviewWindow : opt →Period  derived SHOULD    -- the review window of NICE CG150 rec. 1.3.48
}
-- wholePeriodFrom(d, p): a whole calendar month, 28-day period or calendar week that begins on d ends on or before the end of p
pred wholePeriodFrom(d : Date, p : Period) ≙ ∃ g : Granularity; e : Date • d ≤ e ∧ e ≤ p.end ∧ ofKind(d, e, g)
-- reviewWindowFromWeeks, reviewWindowToWeeks, followUpMonths: table SD-FX
```
- Meaning: For a patient withdrawing from overused medication, headache days and acute-medication days from the start of withdrawal onward, for the period the view covers and for each whole period of a series that begins on the start of withdrawal, including the review window 4 to 8 weeks after the start of withdrawal named in NICE CG150 recommendation 1.3.48, continued over the following year, with a label of the expected transient worsening in the early withdrawal phase. `wholePeriodFrom(d, p)` holds when a whole calendar month, 28-day period or calendar week that begins on d ends within p.
- Conformance: Availability: SHOULD (INV-049); applicability: "For patients withdrawing from overused medication", each start in `ctx.subject.withdrawalStart`. Content: SHOULD (INV-050). Definitional: INV-051, INV-123. Labels and caveats: C3-06. Placement: `series` (W2, SHOULD).
- Realises: OUT-017
- Evidence: Stage 1 OUT-017; [S-015] E-039/Q00.
- Notes: Relations: INV-051, INV-123. See ISS-11. Rationale: E-039/D01, E-039/D02, E-039/D03, E-039/D04.

### 5.5 Preventive treatment response

### E-040 Change
- Definition:
```omn
element Change extends Item {
  reference : →DayCount  core  shown MUST when ofResponseComparison(self)   -- the value of the reference (baseline) period
  compared : →DayCount  core  shown MUST when ofResponseComparison(self)    -- the value of the compared period
  absolute : opt ℤ  derived MUST when ofResponseComparison(self)              -- the absolute change; unit: days
  relative : opt RelativeChange  derived MUST when ofResponseComparison(self)  -- the percentage change
}
variant RelativeChange ::= percent ⟨ℚ⟩ | undefinedForZeroReference      -- unit of percent: %
pred ofResponseComparison(ch : Change) ≙ ∃ rc : ResponseComparison • ch ∈ rc.changes   -- a response comparison shows the change
```
- Meaning: The change of a day count between a reference (baseline) period and a compared period, shown as an absolute change, as a percentage change, or both. When the reference value is 0, a percentage change does not exist, and a change that shows its percentage form says so. `ofResponseComparison(ch)` holds when ch is one of the changes that a response comparison shows (E-043); by rule W1 that comparison belongs to the same output as the change.
- Conformance: Availability: none of its own. Content: INV-060, INV-097 (SHOULD); its values: INV-003 (MUST), INV-008, INV-011 (SHOULD) (`referencedValues`, E-011). Definitional: INV-053, INV-111. Placement: `reference`, `compared` (W2, MUST, `when ofResponseComparison(self)`).
- Realises: OUT-018, OUT-019, OUT-020, OUT-036
- Evidence: Stage 1 OUT-018 ("showing both the values of each period and the absolute and percentage change from baseline"), OUT-019 ("Wherever the output shows a relative (percentage) change in migraine or headache days"), OUT-020 (the underlying values of a responder label), OUT-036 (c).
- Notes: Relations: INV-053. Rationale: E-040/D01.

### E-041 EvaluationRule
- Definition:
```omn
value EvaluationRule {
  guidance : Text                            -- the guidance and recommendation as the output names it
  headacheType : HeadacheType                -- the headache type whose preventive treatment the guidance concerns
  ages : AgeCoverage                         -- the ages of the people the guidance covers
  appliesTo : set1 PreventiveTreatmentType   -- the preventive treatment types the time point is named for
  excludes : set PreventiveTreatmentType     -- for a rule named for all preventive treatment, the types to which the same guidance
                                             --   gives, in a rule of its own for the type, a time point after this rule's time point
                                             --   or window; ∅ for a rule named for particular types
  anchor : AnchorKind
  timing : TimePointTiming
  minOffset : CalendarOffset
  maxOffset : opt CalendarOffset
}
enum AgeCoverage ::= anyAge | aged12AndOver | adultsOnly | childrenAndAdolescentsOnly
variant AnchorKind ::= treatmentStartAnchor | toleratedOrTargetDoseAnchor | endOfCycleAnchor ⟨ℕ₁⟩
enum TimePointTiming ::= atOffset | atLeastOffset | withinWindow
variant CalendarOffset ::= weeks ⟨ℕ⟩ | months ⟨ℕ⟩
fun shift : Date × CalendarOffset → Date
axiom ∀ d : Date; n : ℕ • shift(d, weeks(n)) = plusDays(d, 7 × n) ∧ shift(d, months(n)) = plusMonths(d, n)
const allPreventiveTypes : set1 PreventiveTreatmentType ≙ {doseTitratedPreventive, fixedDosePreventive, oralPreventive, cgrpInhibitor,
  antiCGRPMonoclonalAntibody, monthlyInjectable, quarterlyInjectable, onabotulinumtoxinA, otherPreventive}
const evaluationRules : set1 EvaluationRule ≙ table SD-ER
pred anchorMatches(a : AnchorKind, k : CourseEventKind) ≙
  (a = treatmentStartAnchor ∧ k = start) ∨ (a = toleratedOrTargetDoseAnchor ∧ k = targetDoseReached) ∨
  (∃ n : ℕ₁ • a = endOfCycleAnchor(n) ∧ k = cycleEnd(n))
fun anchorDates(c : OutputContext, t : Treatment, a : AnchorKind) : set Date ≙
  {e ∈ c.subject.courseEvents | e.treatment = t ∧ anchorMatches(a, e.kind) • e.date}
pred ageCovered(c : OutputContext, a : AgeCoverage, d : Date) ≙
  (a = aged12AndOver ⇒ c.subject.aged12From ≤ d) ∧ (a = adultsOnly ⇒ ¬ childOn(c, d)) ∧
  (a = childrenAndAdolescentsOnly ⇒ childOn(c, d))
pred inPopulation(c : OutputContext, t : Treatment, r : EvaluationRule) ≙
  (∃ h : HeadacheType • (t, h) ∈ c.subject.preventiveFor ∧ h ⊑ r.headacheType) ∧ ∃ s ∈ startOf(c, t) • ageCovered(c, r.ages, s)
pred applicable(c : OutputContext, t : Treatment, r : EvaluationRule) ≙
  t ∈ c.subject.preventiveTreatments ∧ inPopulation(c, t, r) ∧
  (∃ ty ∈ r.appliesTo • (t, ty) ∈ c.subject.preventiveTypes) ∧ (¬ ∃ ty ∈ r.excludes • (t, ty) ∈ c.subject.preventiveTypes) ∧
  anchorDates(c, t, r.anchor) ≠ ∅
```
- Meaning: The evaluation time points named in current guidance, which differ by treatment type, each with the population its guidance addresses: the headache type whose preventive treatment the guidance concerns (`headacheType`; migraine, `c1`, for every rule of the list) and the ages it covers (`ages`). `atOffset`: the time point is the date `shift(anchor, minOffset)`; `atLeastOffset`: the earliest time point is that date, for a single offset worded as a minimum ("a minimum of", "wait" … "before", "минимум"), or for a minimum number of administrations, from the end of the treatment cycle of the last of them (Turkish section 7.3; E-041/D05); `withinWindow`: the time point lies between the two offsets, for a range of offsets, also where the range is worded as a minimum ("3 to 6 months", "at least 8–12 weeks", "niet eerder dan na 2-3 maanden", "en az 2-3 ay"; E-041/D05). In each case a time point is a date on which the evaluation falls: the first day after the interval that the offset names, an interval whose first day is the anchor date (for an anchor at the end of a treatment cycle with no further offset, the date of that end itself, which is the first day after the cycle, E-008); an on-treatment period evaluated at it ends on the day before, with the interval (`atTimePoint`, E-042; day convention, section 2.8). `excludes` lists, for a rule named for all preventive treatment, each type to which the same guidance gives, in another rule of the list that it names for that type and not for all preventive treatment, a time point that lies after this rule's time point or, for a window, after its latest date: the guidance's statement for that type is the more specific one, and this rule would place an assessment of a treatment of that type before the guidance's own time point for it, so it does not apply to such a treatment. `ageCovered(c, a, d)` holds when the subject is, on the date d, of the ages a covers: any age (`anyAge`), aged 12 years or older (`aged12AndOver`), an adult (`adultsOnly`), or a child or adolescent (`childrenAndAdolescentsOnly`). `inPopulation(c, t, r)` holds when the preventive treatment t is given for a headache type that is the rule's headache type or a subtype of it (`preventiveFor`, E-008) and the subject was, on the start of t, of the ages the rule's guidance covers. `applicable(c, t, r)` holds when, in addition, t is of a type the rule names and of no type it excludes, and has the rule's anchor.
- Conformance: Structural (a value set: table SD-ER); used by E-042, E-043, INV-055, INV-058, INV-059.
- Realises: OUT-018, OUT-036
- Evidence: Stage 1 OUT-018, OUT-036; [S-008], [S-011], [S-015], [S-016], [S-018], [S-028], [S-033], [S-034], [S-035] E-041/Q00, [S-015] E-041/Q01, [S-015] E-041/Q02, [S-015] E-041/Q03, [S-015] E-041/Q04, [S-018] E-041/Q05, [S-018] E-041/Q06, [S-018] E-041/Q07, [S-016] E-041/Q08, [S-016] E-041/Q09, [S-011] E-041/Q10, [S-011] E-041/Q11, [S-008] E-041/Q12, [S-008] E-041/Q13, [S-008] E-041/Q14, [S-028] E-041/Q15, [S-033] E-041/Q16, [S-033] E-041/Q17, [S-033] E-041/Q18, [S-034] E-041/Q19, [S-034] E-041/Q20, [S-034] E-041/Q21, [S-035] E-041/Q22, [S-035] E-041/Q23, [S-035] E-041/Q24, [S-035] E-041/Q25, [S-035] E-041/Q26, [S-035] E-041/Q27, [S-035] E-041/Q28, [S-015] E-041/Q29, [S-106] E-041/Q30.
- Notes: See ISS-10. R-MCF (1). Rationale: E-041/D01, E-041/D02, E-041/D03, E-041/D04, E-041/D05, E-041/D06, E-041/N01.

### E-042 EvaluationTimePoint
- Definition:
```omn
element EvaluationTimePoint extends Item {
  rule : EvaluationRule  core
  treatment : Treatment  core
  anchorDate : Date  MUST                 -- the treatment start, the date the tolerated or target dose was reached, or the end of a treatment cycle
  earliest : Date  derived MUST           -- the date on which the evaluation falls (for a window, its first date)
  latest : opt Date  derived MUST when self.rule.maxOffset ≠ ∅    -- the last date of a window
}
-- atTimePoint(p, tp): p ends at the time point, its last day being the day before the date on which the evaluation falls
pred atTimePoint(p : Period, tp : EvaluationTimePoint) ≙
  (tp.rule.timing ∈ {atOffset, atLeastOffset} ⇒ next(p.end) = tp.earliest) ∧
  (tp.rule.timing = withinWindow ⇒ tp.earliest ≤ next(p.end) ∧ ∀ l ∈ tp.latest • next(p.end) ≤ l)
-- shortestMonthlyDays: table SD-FX
pred fitsMonthlyPeriod(s : Date, a : Date, r : EvaluationRule) ≙
  (r.timing ∈ {atOffset, atLeastOffset} ⇒ plusDays(s, shortestMonthlyDays) ≤ shift(a, r.minOffset)) ∧
  (r.timing = withinWindow ⇒ ∀ x ∈ r.maxOffset • plusDays(s, shortestMonthlyDays) ≤ shift(a, x))
-- notStoppedBefore(c, t, d): no stop or pause of the course of treatment t is dated before d; a stop or pause being dated on the
-- last day of the course (section 2.8), the course has not ended before d
pred notStoppedBefore(c : OutputContext, t : Treatment, d : Date) ≙
  ¬ ∃ e ∈ c.subject.courseEvents • e.treatment = t ∧ e.kind is stop ∧ e.date < d
-- intervalOnTreatment(c, t, a, r): the course of t has not ended before the last day of the interval that rule r names from the
-- anchor date a, the day before its time point (for a window, the day before its first date)
pred intervalOnTreatment(c : OutputContext, t : Treatment, a : Date, r : EvaluationRule) ≙
  notStoppedBefore(c, t, plusDays(shift(a, r.minOffset), −1))
```
- Meaning: An evaluation time point of a guidance rule for one preventive treatment, shown with the response comparison: the guidance it comes from, its anchor date, and the date (or window) on which the evaluation falls, the first day after the interval that the guidance names (day convention, section 2.8). `atTimePoint(p, tp)` holds when the on-treatment period p ends at the time point: its last day is the day before the date on which the evaluation falls (for a window, the day after its last day lies within the window), so that p ends with the interval, the n weeks or n months from the anchor date or the named treatment cycles. `fitsMonthlyPeriod(s, a, r)` holds when a calendar month or 28-day period that begins on or after the treatment start s can end at the time point of rule r anchored at a (for a window, at a date within the window): such a period has at least 28 days (E-005), so its last day is no earlier than 27 days after s, and the date at which it ends no earlier than 28 days after s. `notStoppedBefore(c, t, d)` holds when no stop or pause of the course of t is dated before d: a stop or pause is dated on the last day of the course (section 2.8), so the course has not ended before d, and a period that ends on d lies within the course where it begins on or after the start. `intervalOnTreatment(c, t, a, r)` holds when the course has not ended before the last day of the interval that rule r names from the anchor date a, the day before the time point (for a window, the day before its first date): the course is taken through the interval that the time point closes.
- Conformance: Content of E-043: MUST (INV-059). Definitional: INV-058.
- Realises: OUT-018
- Evidence: Stage 1 OUT-018, OUT-001, OUT-036; [S-005], [S-011], [S-015] E-042/Q00.
- Notes: Relations: INV-058; `fitsMonthlyPeriod` and `intervalOnTreatment` are used in INV-055 and INV-059. R-MCF (1). Rationale: E-042/D01, E-042/W01, E-042/W02.

### E-043 ResponseComparison
- Definition:
```omn
element ResponseComparison extends Item {
  treatment : Treatment  core
  treatmentStart : Date  MUST                  -- the date the comparison is aligned to
  baseline : →Period  MUST                     -- the pre-treatment baseline month: a calendar month or 28-day period
  onTreatment : seq1 →Period  MUST             -- calendar months or 28-day periods after treatment start, earliest first
  values : set1 →DayCount  MUST                -- the values of each compared period
  changes : set1 →Change  MUST                 -- absolute and percentage change from baseline for each on-treatment period
  timePoints : set →EvaluationTimePoint  MUST when ∃ r ∈ evaluationRules; a ∈ anchorDates(ctx, self.treatment, r.anchor) •
      applicable(ctx, self.treatment, r) ∧ intervalOnTreatment(ctx, self.treatment, a, r)  shown MUST
}
```
- Meaning: For one preventive treatment, monthly migraine days and monthly headache days (and, where the diary reports them, moderate/severe headache days) in a pre-treatment baseline month compared with monthly periods after the treatment start, aligned to the treatment start date, showing the values of each period and the absolute and percentage change from baseline, with the guidance evaluation time points.
- Conformance: Availability: MUST (INV-055); applicability: "For each preventive treatment", whose start the context states — R-MCF (1). Content: MUST (INV-056, INV-057, INV-059). Definitional: INV-123. Prohibited: C2-05 (MUST NOT). Placement: `timePoints` (W2, MUST).
- Realises: OUT-001, OUT-018, OUT-036
- Evidence: Stage 1 OUT-001, OUT-018, OUT-036.
- Notes: Several consecutive or separate monthly on-treatment periods may be compared with the same baseline month. See ISS-03, ISS-10. R-MCF (1). Rationale: E-043/D01.

### E-044 ResidualBurden
- Definition:
```omn
element ResidualBurden extends Item {
  change : →Change  core                         -- the change it refers to; shown next to it where INV-060 requires
  migraineDays : →DayCount  core                 -- migraine days per month that remain on treatment
  moderateSevereHeadacheDays : →DayCount  core   -- moderate/severe headache days per month that remain on treatment
}
```
- Meaning: Next to a percentage change in migraine or headache days, the absolute numbers of migraine days and of moderate/severe headache days per month that remain on treatment, so that a large percentage reduction does not hide a substantial number of disabling days.
- Conformance: Content: SHOULD (INV-060). Definitional: INV-061.
- Realises: OUT-019
- Evidence: Stage 1 OUT-019.
- Notes: Relations: INV-061. See ISS-03, ISS-05. Rationale: E-044/D01.

### E-045 ResponderCriterion
- Definition:
```omn
value ResponderCriterion {
  name : Text                                    -- the criterion as the output names it
  components : set1 CriterionComponent           -- any one or more of the components makes the criterion met
  alsoRestsOn : set UnderlyingKind               -- the kinds of value on which the criterion also rests, besides the day counts and
                                                 --   changes of the response comparison, the residual burden and the control-level count
} where (∀ s : ScoreComponent • scoreDecrease(s) ∈ components ⇒ instrumentResultOf(s.instrument) ∈ alsoRestsOn) ∧
  (∀ a : AttackReductionComponent • attackReduction(a) ∈ components ⇒
     (a.headacheType = ∅ ⇒ periodValuesOf(eventCountsOf(attacks)) ∈ alsoRestsOn) ∧
     (∀ t ∈ a.headacheType • typeValuesOf((eventCountsOf(attacks), t)) ∈ alsoRestsOn))
variant CriterionComponent ::= reductionFromBaseline ⟨ReductionComponent⟩ | attackReduction ⟨AttackReductionComponent⟩
  | scoreDecrease ⟨ScoreComponent⟩ | judgement ⟨Text⟩ | controlLevels
value ReductionComponent { measures : set1 DayMeasure; atLeastPercent : Percent; condition : SubjectCondition }   -- the measures
                                                 --   over all headache types combined
value AttackReductionComponent { atLeastPercent : Percent; condition : SubjectCondition;   -- a reduction in the number of attacks
  headacheType : opt HeadacheType }              -- the headache type whose attacks it counts; ∅: the attacks of all types combined
value ScoreComponent { instrument : Instrument; decrease : ScoreDecrease; baselineAtLeast : opt ℚ; baselineAtMost : opt ℚ;
  condition : SubjectCondition }
variant ScoreDecrease ::= atLeastPoints ⟨ℚ⟩ | atLeastPercentOfBaseline ⟨Percent⟩
variant SubjectCondition ::= anySubject | episodicMigraineOnly | chronicMigraineOnly | ihsQ6ChronicAlternativeOnly
                                                 -- conditions read on the treatment a label refers to (conditionHolds)
variant UnderlyingKind ::= instrumentResultOf ⟨Instrument⟩ | acuteTreatmentEffectiveness
  | periodValuesOf ⟨PeriodValueKind⟩      -- per-period values of the kind over all headache types combined, for the baseline and
                                          --   each evaluated period
  | typeValuesOf ⟨PeriodValueKind × HeadacheType⟩   -- per-period values of the kind for the subject's headaches of one headache
                                          --   type (scope `scopeFor`, E-012), for the baseline and each evaluated period
  | otherValueNamed ⟨Text⟩                -- a value of any other kind, named as the output names it
variant PeriodValueKind ::= dayCountsOf ⟨DayMeasure⟩ | eventCountsOf ⟨CountedEvent⟩ | intensitySummaries
  | durationSummariesOf ⟨DurationKind⟩ | symptomPresenceOf ⟨AssociatedSymptom⟩ | mostBothersomeSymptoms
  | caregiverImpacts | compositeIndicesOf ⟨HeadacheIndexKind⟩ | acuteTreatmentSummaries
fun showsValueNamed : Item × Text → 𝔹           -- showsValueNamed(x, t): the item x shows a value of the kind that t names
pred valueOfKind(m : PeriodValue, k : PeriodValueKind) ≙
  (∃ d : DayMeasure; x ∈ {m} ∩ DayCount • k = dayCountsOf(d) ∧ x.measure = d) ∨
  (∃ ev : CountedEvent; x ∈ {m} ∩ EventCount • k = eventCountsOf(ev) ∧ x.event = ev) ∨
  (k = intensitySummaries ∧ m ∈ IntensitySummary) ∨
  (∃ dk : DurationKind; x ∈ {m} ∩ DurationSummary • k = durationSummariesOf(dk) ∧ x.kind = dk) ∨
  (∃ sy : AssociatedSymptom; x ∈ {m} ∩ AssociatedSymptomSummary • k = symptomPresenceOf(sy) ∧ x.symptom = sy) ∨
  (k = mostBothersomeSymptoms ∧ m ∈ MostBothersomeSymptomItem) ∨ (k = caregiverImpacts ∧ m ∈ CaregiverImpact) ∨
  (∃ ik : HeadacheIndexKind; x ∈ {m} ∩ CompositeIndex • k = compositeIndicesOf(ik) ∧ x.index = ik) ∨
  (k = acuteTreatmentSummaries ∧ m ∈ AcuteTreatmentSummary)
pred conditionHolds(c : OutputContext, t : Treatment, s : SubjectCondition) ≙
  (s = episodicMigraineOnly ⇒ givenFor(c, t, c1) ∧ ¬ givenFor(c, t, c1_3)) ∧ (s = chronicMigraineOnly ⇒ givenFor(c, t, c1_3)) ∧
  (s = ihsQ6ChronicAlternativeOnly ⇒ t ∈ c.subject.ihsQ6ChronicAlternative)
pred valueAvailable(c : OutputContext, u : UnderlyingKind) ≙
  (∀ ins : Instrument • u = instrumentResultOf(ins) ⇒ ∃ a ∈ c.subject.instrumentAdministrations • a.instrument = ins) ∧
  (u = acuteTreatmentEffectiveness ∨ u = periodValuesOf(acuteTreatmentSummaries) ∨
     (∃ h : HeadacheType • u = typeValuesOf((acuteTreatmentSummaries, h))) ⇒ c.subject.acuteMedications ≠ ∅) ∧
  (∀ k : PeriodValueKind • u = periodValuesOf(k) ⇒ provides({m : PeriodValue | valueOfKind(m, k)})) ∧
  (∀ k : PeriodValueKind; h : HeadacheType • u = typeValuesOf((k, h)) ⇒
     provides({m : PeriodValue | valueOfKind(m, k)}) ∧ mayHaveType(c, h)) ∧
  (∀ t : Text • u = otherValueNamed(t) ⇒ provides({x : Item | showsValueNamed(x, t)}))
const namedCriteria : set1 ResponderCriterion ≙ table SD-RC
```
- Meaning: A named responder criterion with its thresholds, as an output shows it next to a responder label: a criterion is met when any one of its components is met. `reductionFromBaseline`: a reduction from baseline of at least the stated percentage in one of the listed day measures over all headache types combined, where the label's treatment meets the condition; `attackReduction`: a reduction from baseline of at least the stated percentage in the number of attacks (E-019) of the subject's headaches of the headache type the component names (`headacheType`, in the scope `scopeFor` of E-012), or of all headache types combined where it names none, where the label's treatment meets the condition; `scoreDecrease`: a decrease of an instrument score, from the pre-treatment baseline score to the score at the evaluation (E-046), of at least the stated points or percentage of the baseline score, for baseline scores in the stated range and where the label's treatment meets the condition; `judgement`: a component that rests on a clinical or patient judgement, or on values for which the criterion states no threshold that a shown value can be tested against, shown by its wording; `controlLevels`: the four control levels of the IHS position statement 2025 (E-046, INV-064). `alsoRestsOn` lists the kinds of value on which the criterion also rests, besides the day counts and changes of the label's response comparison (OUT-018), its residual burden (OUT-019) and, for control levels, the count of E-018 (INV-062): the results of an instrument (`instrumentResultOf`), the effectiveness of each acute medication the subject has used, over all headache types combined, in each evaluated period (`acuteTreatmentEffectiveness`), per-period values of a kind over all headache types combined (`periodValuesOf`) or for the subject's headaches of one headache type (`typeValuesOf`, in the scope `scopeFor` of E-012), which the label shows for the baseline period of its response comparison and for each evaluated period, and a value of any other kind, named as the output names it (`otherValueNamed`). `PeriodValueKind` names the kinds of per-period value of the model on which a criterion can rest (E-045/D07): each kind of day count (E-014, including acute-medication days and functional-impact days), attack and aura counts (E-019), intensity summaries (E-023), duration summaries of each kind (E-024), the presence of each associated symptom (E-025), the most bothersome symptom (E-026), caregiver impact (E-031), composite indices of each kind (E-033) and acute-treatment summaries (E-051); `valueOfKind(m, k)` holds when the per-period value m is of kind k. `showsValueNamed(x, t)` holds when the item x shows a value of the kind that the text t names, for example a treatment line that shows the adverse effects of the treatment (E-055) for a criterion that names them. The `where` clause makes a criterion list the instrument of each of its score components and, where it has an attack-reduction component, the attack counts of the headache types whose attacks the component counts. `valueAvailable(c, u)` holds when a value of kind u on which a criterion also rests can exist for the subject: a result of the instrument is available (the condition of OUT-026, "Where results of validated instruments are available"); for the effectiveness of acute treatment, or acute-treatment summaries, the subject has used acute medication up to the as-of date (OUT-023, "For each acute medication"); for per-period values of a kind, or a value of another kind, the diary provides values of that kind (`provides`, the "where provided" of section 3.5), and, for the values of one headache type, the subject has or may have that type (`mayHaveType`, E-008).
- Conformance: Structural (a value set: table SD-RC). Content: INV-062 (SHOULD). Definitional: INV-116.
- Realises: OUT-018, OUT-020
- Evidence: Stage 1 OUT-020, OUT-018, OUT-011, OUT-021, OUT-023, OUT-010, OUT-006, OUT-004; [S-001], [S-008], [S-015], [S-023], [S-030], [S-032], [S-033], [S-035], [S-042] E-045/Q00, [S-008] E-045/Q01, [S-008] E-045/Q02, [S-010] E-046/Q01 to E-046/Q05, [S-035] E-045/Q03, [S-035] E-045/Q04.
- Notes: Relations: INV-116. The evaluation time point that [S-033] attaches to `critRu71` ("через 3 месяца терапии") is the rule `ruleRu71` of E-041. Rationale: E-045/D01, E-045/D02, E-045/D03, E-045/D04, E-045/D05, E-045/D06, E-045/D07, E-045/D08, E-045/D09, E-045/N01, E-045/N02.

### E-046 ResponderLabel
- Definition:
```omn
element ResponderLabel extends Item {
  category : ResponderCategory  core
  treatment : Treatment  core
  evaluated : seq1 →Period  core                  -- the on-treatment period or periods the label refers to
  criterion : opt ResponderCriterion  SHOULD       -- the named criterion, shown with its thresholds
  comparison : opt →ResponseComparison  SHOULD  shown SHOULD     -- the underlying values (OUT-018)
  residual : set →ResidualBurden  SHOULD  shown SHOULD           -- the residual burden (OUT-019)
  otherValues : set →Item  SHOULD when ∃ k ∈ self.criterion • ∃ u ∈ k.alsoRestsOn • valueAvailable(ctx, u)  shown SHOULD   -- the other values the criterion rests on
}
variant ResponderCategory ::= responder | nonResponder | controlLevel ⟨ControlLevel⟩
enum ControlLevel ::= migraineFreedom | optimalControl | modestControl | insufficientControl
pred reductionMet(L : ResponderLabel, r : ReductionComponent) ≙ #L.evaluated = 1 ∧ conditionHolds(ctx(outputOf(L)), L.treatment, r.condition) ∧
  ∃ rc ∈ L.comparison; ch ∈ rc.changes • rc.treatment = L.treatment ∧ ch.reference.period = rc.baseline ∧
    (∃ p ∈ ran L.evaluated • sameSpan(ch.compared.period, spanOf(p))) ∧ ch.reference.measure ∈ r.measures ∧
    ch.reference.typeScope = allTypes ∧
    ch.reference.days > 0 ∧ 100 × (ch.reference.days − ch.compared.days) ≥ r.atLeastPercent × ch.reference.days
pred reductionDecided(L : ResponderLabel, r : ReductionComponent) ≙ ¬ conditionHolds(ctx(outputOf(L)), L.treatment, r.condition) ∨
  (#L.evaluated = 1 ∧ ∀ k ∈ r.measures; p ∈ ran L.evaluated • ∃ rc ∈ L.comparison; ch ∈ rc.changes • rc.treatment = L.treatment ∧
    ch.reference.period = rc.baseline ∧ ch.reference.measure = k ∧ sameSpan(ch.compared.period, spanOf(p)) ∧
    ch.reference.typeScope = allTypes ∧ ch.reference.days > 0)
-- evaluationResult(L, r): r is the latest available result of its instrument that was completed after the treatment start shown
-- in the label's response comparison and within the last period the label refers to
pred evaluationResult(L : ResponderLabel, r : InstrumentResult) ≙
  ∃ rc ∈ L.comparison; d ∈ r.completionDate • rc.treatment = L.treatment ∧ rc.treatmentStart < d ∧ inPeriod(d, last(L.evaluated)) ∧
    ¬ ∃ a ∈ ctx(outputOf(L)).subject.instrumentAdministrations • a.instrument = r.instrument ∧ d < a.date ∧ inPeriod(a.date, last(L.evaluated))
-- pretreatmentBaseline(L, b): b is the latest available result of its instrument that was completed on or before that treatment start
pred pretreatmentBaseline(L : ResponderLabel, b : InstrumentResult) ≙
  ∃ rc ∈ L.comparison; d ∈ b.completionDate • rc.treatment = L.treatment ∧ d ≤ rc.treatmentStart ∧
    ¬ ∃ a ∈ ctx(outputOf(L)).subject.instrumentAdministrations • a.instrument = b.instrument ∧ d < a.date ∧ a.date ≤ rc.treatmentStart
pred scoreMet(L : ResponderLabel, s : ScoreComponent) ≙ conditionHolds(ctx(outputOf(L)), L.treatment, s.condition) ∧
  ∃ r ∈ L.otherValues ∩ InstrumentResult; b ∈ r.baselineResult; x ∈ r.totalScore; y ∈ b.totalScore •
    r.instrument = s.instrument ∧ evaluationResult(L, r) ∧ pretreatmentBaseline(L, b) ∧
    (∀ lo ∈ s.baselineAtLeast • y ≥ lo) ∧ (∀ hi ∈ s.baselineAtMost • y ≤ hi) ∧
    ((∃ n : ℚ • s.decrease = atLeastPoints(n) ∧ y − x ≥ n) ∨
     (∃ pc : Percent • s.decrease = atLeastPercentOfBaseline(pc) ∧ y > 0 ∧ 100 × (y − x) ÷ y ≥ pc))
pred scoreDecided(L : ResponderLabel, s : ScoreComponent) ≙ ¬ conditionHolds(ctx(outputOf(L)), L.treatment, s.condition) ∨
  ∃ r ∈ L.otherValues ∩ InstrumentResult; b ∈ r.baselineResult • r.instrument = s.instrument ∧
    evaluationResult(L, r) ∧ pretreatmentBaseline(L, b) ∧ r.totalScore ≠ ∅ ∧ b.totalScore ≠ ∅
-- attackScope(c, a, sc): sc is the type scope of the attacks that the attack-reduction component a counts: all headache types
-- combined, or the subject's headaches of the headache type it names (scopeFor, E-012)
pred attackScope(c : OutputContext, a : AttackReductionComponent, sc : TypeScope) ≙
  (a.headacheType = ∅ ∧ sc = allTypes) ∨ (∃ t ∈ a.headacheType • scopeFor(c, sc, t))
-- attackReductionMet(L, a): the attack counts that the label shows for the baseline period of its response comparison and for its
-- single evaluated period (periods with these dates), both of the type scope of the attacks the component counts, fall by at least
-- the threshold
pred attackReductionMet(L : ResponderLabel, a : AttackReductionComponent) ≙ #L.evaluated = 1 ∧ conditionHolds(ctx(outputOf(L)), L.treatment, a.condition) ∧
  ∃ rc ∈ L.comparison; b, f ∈ L.otherValues ∩ AttackCount • rc.treatment = L.treatment ∧ sameSpan(b.period, spanOf(rc.baseline)) ∧
    (∃ p ∈ ran L.evaluated • sameSpan(f.period, spanOf(p))) ∧ attackScope(ctx(outputOf(L)), a, b.typeScope) ∧
    f.typeScope = b.typeScope ∧ b.count > 0 ∧
    100 × (b.count − f.count) ≥ a.atLeastPercent × b.count
pred attackReductionDecided(L : ResponderLabel, a : AttackReductionComponent) ≙ ¬ conditionHolds(ctx(outputOf(L)), L.treatment, a.condition) ∨
  (#L.evaluated = 1 ∧ ∃ rc ∈ L.comparison; b, f ∈ L.otherValues ∩ AttackCount • rc.treatment = L.treatment ∧
    sameSpan(b.period, spanOf(rc.baseline)) ∧ (∃ p ∈ ran L.evaluated • sameSpan(f.period, spanOf(p))) ∧
    attackScope(ctx(outputOf(L)), a, b.typeScope) ∧ f.typeScope = b.typeScope ∧ b.count > 0)
pred componentMet(L : ResponderLabel, k : CriterionComponent) ≙
  (∃ r : ReductionComponent • k = reductionFromBaseline(r) ∧ reductionMet(L, r)) ∨
  (∃ a : AttackReductionComponent • k = attackReduction(a) ∧ attackReductionMet(L, a)) ∨ (∃ s : ScoreComponent • k = scoreDecrease(s) ∧ scoreMet(L, s))
pred componentDecided(L : ResponderLabel, k : CriterionComponent) ≙
  (∃ r : ReductionComponent • k = reductionFromBaseline(r) ∧ reductionDecided(L, r)) ∨
  (∃ a : AttackReductionComponent • k = attackReduction(a) ∧ attackReductionDecided(L, a)) ∨
  (∃ s : ScoreComponent • k = scoreDecrease(s) ∧ scoreDecided(L, s))
fun levelDays(L : ResponderLabel, p : Period) : set ℕ ≙ daysOf(viewOf(L), migraineOrModerateSevereHeadacheDays, p, allTypes)
-- evaluatedOnTreatment(L): every period the label refers to ends on or before the date of every stop or pause of its treatment,
-- the last day of the course (section 2.8), so that no evaluated period reaches past the end of the course
pred evaluatedOnTreatment(L : ResponderLabel) ≙ ∀ p ∈ ran L.evaluated • notStoppedBefore(ctx(outputOf(L)), L.treatment, p.end)
pred inControlRange(k : ControlLevel, n : ℕ) ≙ table SD-CL             -- the number n of days of a month lies in the range of level k
fun controlMinMonths(k : ControlLevel) : set ℕ₁ ≙ table SD-CL default ∅  -- the least number of evaluated months for level k
fun forcedAbove(k : ControlLevel) : set ℕ ≙ table SD-CL default ∅        -- days above which, in every evaluated month, level k applies
```
- Meaning: An optional label that classifies the response to a preventive treatment under a named criterion: responder or non-responder, or a control level of the IHS position statement 2025. It is shown with the criterion it applies, the values it rests on, and the residual burden, and it is not presented as the sole indicator of individual benefit. `evaluationResult(L, r)` holds when r is the latest available result of its instrument that was completed after the treatment start shown in the label's response comparison and within the last period the label refers to; `pretreatmentBaseline(L, b)` holds when b is the latest available result of its instrument that was completed on or before that treatment start. `attackScope(c, a, sc)` holds when sc is the type scope of the attacks that the attack-reduction component a counts (E-045). `evaluatedOnTreatment(L)` holds when every period the label refers to ends on or before the date of every stop or pause of its treatment, the last day of the course (`notStoppedBefore`, E-042; section 2.8).
- Conformance: Availability: MAY ("If the output displays a responder or non-responder label"). Content: SHOULD (INV-062). Definitional: INV-063, INV-064, INV-114, INV-116, INV-123. Labels and caveats: C3-07. Prohibited: C2-06; C2-05 (MUST NOT). Placement: `comparison`, `residual`, `otherValues` (W2, SHOULD).
- Realises: OUT-020, OUT-025, OUT-038
- Evidence: Stage 1 OUT-020. Control levels, not stated in Stage 1: [S-010] E-046/Q01, [S-010] E-046/Q02, [S-010] E-046/Q03, [S-010] E-046/Q04, [S-010] E-046/Q05.
- Notes: Relations: INV-063, INV-064, INV-114, INV-116, INV-123. See ISS-08. R-MCF (1), (4). Rationale: E-046/D01, E-046/D02, E-046/D03, E-046/D04, E-046/D05, E-046/D06.

### E-047 AdherenceSummary
- Definition:
```omn
element AdherenceSummary extends Item {
  treatment : Treatment  core
  window : →Period  core                         -- the evaluation window the adherence refers to
  adherence : AdherenceValue  derived core
}
variant AdherenceValue ::= proportionOfPrescribedIntake ⟨Percent⟩ | otherAdherenceStatement ⟨Text⟩
-- adherenceFor(a, rc): a shows the adherence to the treatment of rc over an evaluation window of rc: a span that begins on or
-- after the treatment start and contains one of the on-treatment periods of rc, ending with it
pred adherenceFor(a : AdherenceSummary, rc : ResponseComparison) ≙ a.treatment = rc.treatment ∧ rc.treatmentStart ≤ a.window.start ∧
  ∃ p ∈ ran rc.onTreatment • a.window.start ≤ p.start ∧ a.window.end = p.end
```
- Meaning: The patient-reported adherence to the prescribed preventive regimen over the evaluation window, shown next to the response comparison, so that a reader can see whether an apparent lack of effect coincided with inconsistent intake. `adherenceFor(a, rc)` holds when a is the adherence to the treatment of the response comparison rc over an evaluation window of rc: a span that begins on or after the treatment start and contains one of the on-treatment periods of rc, ending with it.
- Conformance: Content: SHOULD (INV-066, INV-104, INV-109). Definitional: INV-067, INV-123.
- Realises: OUT-039
- Evidence: Stage 1 OUT-039.
- Notes: Relations: INV-067, INV-123. Rationale: E-047/D01, E-047/D02.

### E-048 TreatmentReviewView
- Definition:
```omn
element TreatmentReviewView extends View {
  treatment : Treatment  core
  baseline : →Period  MUST
  onTreatment : seq1 →Period  MUST
}
```
- Meaning: For treatment review, headache days, migraine days and acute-medication days (in total across classes, per ICHD-3 8.2 class and per drug, as in OUT-014) presented together for the same pre-treatment baseline and on-treatment periods, with, where provided, moderate/severe headache days, attacks, intensity, migraine-associated symptoms and the most bothersome symptom, the effectiveness of acute treatment for the attacks treated in each of these periods, and the most recent instrument and PGIC results, so that efficacy can be judged across these dimensions and against the patient's own goals.
- Conformance: Availability: MUST (INV-102); applicability: each preventive treatment whose start the context states — R-MCF (1). Content: MUST (INV-068); SHOULD (INV-069, INV-097). Definitional: INV-123.
- Realises: OUT-021, OUT-036
- Evidence: Stage 1 OUT-021, OUT-036 (c).
- Notes: R-MCF (1). Rationale: E-048/D01.

### E-049 PostStopMonitoringView
- Definition:
```omn
element PostStopMonitoringView extends View {
  treatment : Treatment  core
  event : {k : CourseEventKind | k is stop ∨ k = doseChange(reduction)}  core   -- stop(discontinued), stop(paused) or doseChange(reduction)
  eventDate : Date  core
  baseline : opt →Period  SHOULD when originalStart(ctx, self.treatment) ≠ ∅
                                               -- the original pre-treatment baseline period, before the treatment was first started
  onTreatmentPeriod : opt →Period  SHOULD when (∃ s ∈ startOf(ctx, self.treatment); x ∈ firstChangedDay(self.event, self.eventDate) •
      s < x) ∨ (startOf(ctx, self.treatment) = ∅ ∧ ∃ x ∈ firstChangedDay(self.event, self.eventDate) •
      courseBegunBy(ctx, self.treatment, plusDays(x, −1)))   -- an on-treatment period before the changed regimen
  after : seq →Period  SHOULD                  -- consecutive periods from the first day of the changed regimen onward
}
-- firstChangedDay(k, d): the first day of the changed regimen after a course event of kind k dated d: the day after a stop or a
-- pause, which is dated on the last day of the course, and the date of a dose change, the first day at the new dose (section 2.8)
fun firstChangedDay(k : CourseEventKind, d : Date) : set Date ≙ {x : Date | (k is stop ∧ x = next(d)) ∨ (k is doseChange ∧ x = d)}
```
- Meaning: After a preventive treatment is stopped, paused or reduced, headache and migraine frequency continue to be shown and are compared with both the on-treatment period and the original pre-treatment baseline, so that worsening or rebound above baseline is visible. The original pre-treatment baseline is a period that ends before the treatment was first started: before the start of its course or, for a course that resumes the treatment of an earlier course after its stop or pause, before the start of the first course of that chain (`originalStart`, E-008). `firstChangedDay(k, d)` is the first day of the changed regimen after a course event of kind k dated d: the first day off treatment, the day after a stop or pause, which is dated on the last day of the course, and the first day at the reduced dose, the date of a dose reduction (day convention, section 2.8); it has one member for these kinds of event.
- Conformance: Availability: SHOULD (INV-103); applicability: each stop, pause or dose reduction of a preventive treatment, whether or not its start is stated — R-MCF (2). Content: SHOULD (INV-070, INV-097). Definitional: INV-112, INV-123.
- Realises: OUT-022, OUT-036
- Evidence: Stage 1 OUT-022, OUT-036 (c).
- Notes: "Headache and migraine frequency" is represented by headache days and migraine days; see ISS-03. R-MCF (1), (2). Rationale: E-049/D01, E-049/D02, E-049/D03, E-049/D04, E-049/W01, E-049/W02, E-049/W03.

### 5.6 Acute treatment

### E-050 AcuteOutcomeMeasure
- Definition:
```omn
enum EarlyTimePoint ::= twoHours | fifteenMinutes
variant AcuteOutcomeMeasure ::=
    painFreedom ⟨EarlyTimePoint⟩
  | mostBothersomeSymptomAbsent ⟨EarlyTimePoint⟩
  | headacheRelief ⟨EarlyTimePoint⟩                    -- as defined in the IHS acute trial guideline section 1.3.4.5 [S-004]
  | nonPainSymptomsAbsentOrMinimal ⟨EarlyTimePoint⟩    -- absent or minimal disturbances due to migraine-related non-pain symptoms
  | sustainedPainFreedomTo24h
  | headacheReliefMaintainedTo24h
  | nonPainSymptomStatusMaintainedTo24h
  | rescueOrRepeatMedication
  | relapse
  | drugRelatedAdverseEvent
  | adverseEventRegardedMeaningful                      -- the patient regarded a drug-related adverse event as meaningful
fun requiredOutcomes(tp : EarlyTimePoint) : set1 AcuteOutcomeMeasure ≙
  {painFreedom(tp), mostBothersomeSymptomAbsent(tp), headacheRelief(tp), nonPainSymptomsAbsentOrMinimal(tp),
   sustainedPainFreedomTo24h, headacheReliefMaintainedTo24h, nonPainSymptomStatusMaintainedTo24h,
   rescueOrRepeatMedication, relapse, drugRelatedAdverseEvent, adverseEventRegardedMeaningful}
fun earlyTimePointType(k : EarlyTimePoint) : set ICHD3Code ≙ table SD-ET default ∅   -- the headache type whose summaries use k (INV-073)
```
- Meaning: The outcome measures of treated attacks used in the IHS acute trial guideline [S-004], FDA guidance [S-020] and the EHF definitions [S-012]: pain freedom, absence of the most bothersome symptom, headache relief and absent or minimal non-pain-symptom disturbances at the early time point (2 hours; 15 minutes for cluster headache), sustained pain freedom and maintained relief and non-pain-symptom status to 24 hours, use of rescue or repeat medication, relapse, drug-related adverse events and whether the patient regarded them as meaningful.
- Conformance: Structural (a value set; early time points: table SD-ET); used by E-051 to E-053.
- Realises: OUT-012, OUT-023, OUT-031
- Evidence: Stage 1 OUT-023, OUT-031.
- Notes: Rationale: E-050/D01.

### E-051 AcuteTreatmentSummary
- Definition:
```omn
element AcuteTreatmentSummary extends PeriodValue {
  drug : Drug  core
  formulationScope : FormulationScope  core
  formulations : set FormulationOrRoute  SHOULD       -- the formulations or routes of administration it summarises
  earlyTimePoint : EarlyTimePoint  core
  treatedAttacks : ℕ  derived core                    -- number of treated attacks summarised; unit: attacks
  outcomes : set →OutcomeSummary  SHOULD  shown SHOULD
  sequence : seq →TreatedAttackLine  SHOULD when self.treatedAttacks > 0  shown SHOULD   -- the treated attacks it summarises, earliest first
}
enum FormulationScope ::= allFormulations | singleFormulation
-- summarisesMedication(s, m): s summarises the attacks treated with the acute medication m (drug and formulation): it is a
-- summary of m's drug, of all its formulations or of m's formulation only
pred summarisesMedication(s : AcuteTreatmentSummary, m : AcuteMedication) ≙
  s.drug = m.drug ∧ (s.formulationScope = allFormulations ∨ s.formulations = {m.formulation})
```
- Meaning: For one acute medication (all its formulations, or one formulation) and one period, the outcomes across the attacks treated with it, how consistently the drug was effective across consecutive treated attacks (the sequence of per-attack lines), and the formulation or route, so that the EHF definitions of effective attack treatment, triptan response and triptan refractoriness can be applied. Summaries for the pre-treatment baseline period and for the on-treatment periods of a preventive treatment make a change in the response to acute treatment visible. `summarisesMedication(s, m)` holds when s summarises the attacks treated with the acute medication m (a drug and a formulation, E-008): s is a summary of m's drug, of all its formulations or of m's formulation only.
- Conformance: Availability: SHOULD (INV-071); also asked for by INV-062, INV-069, INV-088, INV-104, INV-105, INV-109. Content: SHOULD (INV-072, INV-073). Definitional: INV-074. Prohibited: C2-07. Placement: `outcomes`, `sequence` (W2, SHOULD).
- Realises: OUT-012, OUT-021, OUT-023, OUT-024, OUT-031
- Evidence: Stage 1 OUT-023.
- Notes: Relations: INV-074. Dose changes of acute medications are shown in the treatment history (E-055), as OUT-023 states. Rationale: E-051/D01.

### E-052 OutcomeSummary
- Definition:
```omn
element OutcomeSummary extends Item {
  summary : →AcuteTreatmentSummary  core
  measure : AcuteOutcomeMeasure  core
  attacksWithOutcome : ℕ  derived core      -- unit: attacks
  attacksAssessed : ℕ  derived core         -- treated attacks for which the outcome is shown; unit: attacks
  proportion : opt Percent  derived MAY     -- unit: %
}
```
- Meaning: For one outcome measure, the number of treated attacks summarised with the outcome, out of the treated attacks for which it is shown, and optionally the proportion.
- Conformance: Content of E-051: SHOULD (INV-072). Definitional: INV-074.
- Realises: OUT-023, OUT-031
- Evidence: Stage 1 OUT-023.
- Notes: Relations: INV-074.

### E-053 TreatedAttackLine
- Definition:
```omn
element TreatedAttackLine extends Item {
  onset : Date  core
  drug : Drug  core
  formulation : opt FormulationOrRoute  SHOULD
  results : set AttackOutcomeResult  core
  intakeTiming : opt IntakeTiming  SHOULD                   -- when the medication was taken
  symptomStatus : set SymptomStatus  SHOULD when hasType(ctx, c1)
  adverseEvents : set AdverseEventItem  SHOULD when AttackOutcomeResult(measure ↦ drugRelatedAdverseEvent, achieved ↦ true) ∈ self.results
}
value AttackOutcomeResult { measure : AcuteOutcomeMeasure; achieved : 𝔹 }
variant IntakeTiming ::= timeFromOnset ⟨Duration⟩ | painIntensityAtIntake ⟨ScalePoint⟩
value SymptomStatus { symptom : AssociatedSymptom; presentAtEarlyTimePoint : 𝔹 }
value AdverseEventItem { description : Text; regardedMeaningful : opt 𝔹 }
```
- Meaning: One treated attack, shown by what the output states about it: its date, the medication and formulation taken, the outcome of each measure, when the medication was taken relative to attack onset (or the pain intensity at intake), whether migraine-associated symptoms were present at the early time point, and any drug-related adverse events and whether the patient regarded them as meaningful.
- Conformance: Content of E-051: SHOULD (INV-072, INV-076). Definitional: INV-074, INV-075, INV-123.
- Realises: OUT-012, OUT-023
- Evidence: Stage 1 OUT-012, OUT-023.
- Notes: Relations: INV-074, INV-075, INV-123.

### 5.7 Treatment history and scheme windows

### E-054 TreatmentHistoryView and ClassGroup
- Definition:
```omn
element TreatmentHistoryView extends View {
  preventiveGroups : seq →ClassGroup  SHOULD when ctx.subject.preventiveTreatments ≠ ∅  shown SHOULD
  acuteGroups : seq →ClassGroup  SHOULD when ctx.subject.acuteTreatments ≠ ∅  shown SHOULD
}
element ClassGroup extends Item {
  role : TreatmentRole  core
  drugClass : DrugClass  core
  lines : seq1 →TreatmentLine  core              -- earliest start first
}
enum TreatmentRole ::= preventive | acute
given DrugClass                                    -- the pharmacological class by which the history groups treatments
fun drugClassOf : Drug → DrugClass
```
- Meaning: A chronological list of preventive treatments and, separately, of acute treatments, grouped by drug class. The list shows the treatments that were tried; it does not show drugs that could not be used, nor debilitating days, so it supports but does not by itself establish eligibility for later treatments or for the EHF categories of resistant and refractory migraine (OUT-024 Caveats).
- Conformance: Availability: SHOULD (INV-077). Content: SHOULD (INV-078). Placement: `preventiveGroups`, `acuteGroups` (W2, SHOULD).
- Realises: OUT-024, OUT-039
- Evidence: Stage 1 OUT-024.
- Notes: Rationale: E-054/D01.

### E-055 TreatmentLine
- Definition:
```omn
element TreatmentLine extends Item {
  treatment : Treatment  core
  role : TreatmentRole  core
  drug : Drug  core
  startDate : opt Date  SHOULD when startOf(ctx, self.treatment) ≠ ∅
  stopDate : opt Date  SHOULD when stopped(ctx, self.treatment)
  doseChanges : set DoseChangeItem  SHOULD when hasDoseChange(ctx, self.treatment)
  duration : opt Duration  derived SHOULD when startOf(ctx, self.treatment) ≠ ∅   -- to the stop date or, if not stopped, to the as-of date; unit: days
  preventiveResponse : opt →ResponseComparison  SHOULD when self.role = preventive ∧ startOf(ctx, self.treatment) ≠ ∅  shown SHOULD
  acuteResponse : set →AcuteTreatmentSummary  SHOULD when self.role = acute  shown SHOULD
  adverseEffects : opt AdverseEffects  SHOULD
  stopReason : opt StopReason  SHOULD when stopped(ctx, self.treatment)
  formulations : set FormulationOrRoute  SHOULD when self.role = acute
  adherence : opt →AdherenceSummary  SHOULD when self.role = preventive ∧ startOf(ctx, self.treatment) ≠ ∅  shown SHOULD
}
value DoseChangeItem { date : Date; direction : DoseChangeDirection; newDose : opt Text }
variant AdverseEffects ::= noAdverseEffects | adverseEffectsShown ⟨set1 Text⟩
variant StopReason ::= lackOfEfficacy | adverseEffectsReason | otherStopReason ⟨Text⟩
pred stopped(c : OutputContext, t : Treatment) ≙ ∃ e ∈ c.subject.courseEvents • e.treatment = t ∧ e.kind is stop
pred hasDoseChange(c : OutputContext, t : Treatment) ≙ ∃ e ∈ c.subject.courseEvents • e.treatment = t ∧ e.kind is doseChange
```
- Meaning: One treatment of the history: start and stop dates, dose changes, treatment duration (from the start to the stop or, for a treatment that has not stopped, to the as-of date of the output, that is, its duration to date), the response summary (from OUT-018 for preventive and OUT-023 for acute treatments), adverse effects during the treatment, the reason for stopping, for acute treatments the formulation, and for preventive treatments the adherence (OUT-039).
- Conformance: Content of E-054: SHOULD (INV-077, INV-078, INV-109); the `when` clauses of `startDate`, `duration`, `preventiveResponse` and `adherence`: R-MCF (1). Definitional: INV-079, INV-123. Placement: `preventiveResponse`, `acuteResponse`, `adherence` (W2, SHOULD).
- Realises: OUT-024, OUT-039
- Evidence: Stage 1 OUT-024, OUT-039.
- Notes: Relations: INV-079, INV-123. R-MCF (1). Rationale: E-055/D01, E-055/D02.

### E-056 SchemeWindowView
- Definition:
```omn
element SchemeWindowView extends View {
  scheme : SchemeName  core                     -- shown as the label of the view
  windows : seq1 →Period  core                  -- the evaluation windows the clinician selected
}
```
- Meaning: Frequency, disability and treatment-history outputs for evaluation windows defined by a national reimbursement or monitoring scheme (for example specified treatment weeks, the three months preceding an application, month-by-month responder views or six-monthly reassessments), labelled with the name of the scheme.
- Conformance: Availability: MAY, for contexts with a scheme selection — R-MCF (3). Definitional: INV-080.
- Realises: OUT-025
- Evidence: Stage 1 OUT-025.
- Notes: Relations: INV-080. R-MCF (3). Rationale: E-056/D01.

### 5.8 Instruments

### E-057 Instrument value sets
- Definition:
```omn
variant Instrument ::= midas | hit6 | msq21 | halt90 | halt30 | hurt | mtoq | pedmidas | pgic
  | otherInstrument ⟨OtherInstrumentName⟩         -- another validated impact, disability or quality-of-life instrument
type OtherInstrumentName == {x : Text | x ∉ {"MIDAS", "HIT-6", "MSQ v2.1", "HALT-90", "HALT-30", "HURT", "M-TOQ", "PedMIDAS", "PGIC"}}
fun instrumentName : Instrument → Text
axiom table SD-IN                                   -- instrumentName, publishedRecall, scoreRange and publishedGrading of the named instruments
axiom ∀ x : OtherInstrumentName • instrumentName(otherInstrument(x)) = x
variant RecallPeriod ::= recallMonths ⟨ℕ₁⟩ | recallAsPublished ⟨Text⟩
fun publishedRecall : Instrument ⇸ RecallPeriod
value ScoreRange { low : ℚ; high : opt ℚ }            -- inclusive bounds; high = ∅: the model states no upper bound
fun scoreRange : Instrument ⇸ ScoreRange
const wholeNumberScores : set Instrument ≙ {midas, hit6, pedmidas, halt90, halt30}   -- instruments whose total score is a whole number
value GradeBand { instrument : Instrument; grade : opt Text; label : Text; low : ℚ; strictLow : 𝔹; high : opt ℚ }
pred inBand(x : ℚ, b : GradeBand) ≙ (b.strictLow ⇒ x > b.low) ∧ (¬ b.strictLow ⇒ x ≥ b.low) ∧ ∀ h ∈ b.high • x ≤ h
const gradeBands : set1 GradeBand ≙ table SD-GB
fun publishedGrading : Instrument → 𝔹                -- the instrument's developer publishes a grading or categories
fun banded : Instrument → 𝔹                          -- the model tabulates grade bands for the instrument
axiom ∀ i : Instrument • banded(i) ⇔ (∃ b ∈ gradeBands • b.instrument = i)
```
- Meaning: The instruments named in Stage 1 OUT-026 (MIDAS, HIT-6, MSQ v2.1, HALT, HURT, the Migraine Treatment Optimization Questionnaire, PedMIDAS for children, PGIC) with the parts of their published value sets that the model states: the instrument name as shown, the recall period, the score range, and the grade or category labels with their score bands, exactly as the cited source words them. OUT-026 names these instruments as examples ("Instruments named in the evidence include"), so the set is open: `otherInstrument(x)` is any other validated impact, disability or quality-of-life instrument whose results are available, shown by its name x, which is not the name of one of the nine named instruments; a depression or anxiety screening instrument is a `ScreeningInstrument` (E-059), not an `Instrument`. For instruments whose value sets the model does not tabulate (MSQ v2.1, HURT, M-TOQ, PGIC and every other instrument), results show the instrument's own published scores and categories by name (`recallAsPublished`, `publishedCategory`).
- Conformance: Structural (value sets: tables SD-IN, SD-GB).
- Realises: OUT-026, OUT-036
- Evidence: Stage 1 OUT-026, OUT-036; [S-002], [S-005], [S-014] E-057/Q00, [S-101] E-057/Q01, [S-101] E-057/Q02, [S-102] E-057/Q03, [S-102] E-057/Q04, [S-103] E-057/Q05, [S-014] E-057/Q06, [S-014] E-057/Q07, [S-014] E-057/Q08, [S-014] E-057/Q09, [S-102] E-057/Q10.
- Notes: Relations: INV-082. The cited sources state no upper bound for these instruments, so the model states none: `high = ∅` means that the model states no upper bound, not that the score range has none. See ISS-06. Rationale: E-057/D01, E-057/D02, E-057/D03, E-057/D04, E-057/D05, E-057/D06, E-057/D07, E-057/N01.

### E-058 InstrumentResult
- Definition:
```omn
element InstrumentResult extends Item {
  instrument : Instrument  core                     -- shown by instrumentName
  completionDate : opt Date  SHOULD
  recallPeriod : opt RecallPeriod  SHOULD
  totalScore : opt ℚ  derived SHOULD                -- unit: score points (days for MIDAS, PedMIDAS and HALT)
  category : opt InstrumentCategory  derived SHOULD when publishedGrading(self.instrument)
  baselineResult : opt →InstrumentResult  SHOULD when ∃ d ∈ self.completionDate •
      ∃ a ∈ ctx.subject.instrumentAdministrations • a.instrument = self.instrument ∧ a.date < d   -- the baseline administration
  changeFromBaseline : opt ℚ  derived SHOULD when self.baselineResult ≠ ∅    -- unit: score points
}
variant InstrumentCategory ::= band ⟨GradeBand⟩ | publishedCategory ⟨Text⟩
```
- Meaning: The result of one administration of a validated impact, disability or quality-of-life instrument, one of those named in OUT-026 or another one (`otherInstrument`, E-057): name, completion date, recall period, total score, the instrument's own published grading or categories, and the change from the baseline administration.
- Conformance: Availability: SHOULD (INV-081) — R-MCF (4); PedMIDAS for children and adolescents SHOULD (INV-096). Definitional: INV-082, INV-123. Labels and caveats: C3-08.
- Realises: OUT-020, OUT-021, OUT-025, OUT-026, OUT-034, OUT-036, OUT-038
- Evidence: Stage 1 OUT-026, OUT-036.
- Notes: Relations: INV-082, INV-123. A first administration has no earlier result, so `baselineResult` is required only when an earlier result exists, as in INV-081. See ISS-06. R-MCF (4). Rationale: E-058/D01.

### E-059 ScreeningResult
- Definition:
```omn
element ScreeningResult extends Item {
  instrument : ScreeningInstrument  core
  date : opt Date  SHOULD
  scores : set SubscaleScore  SHOULD
}
variant ScreeningInstrument ::= hads | phq9 | gad7 | otherScreeningInstrument ⟨OtherScreeningName⟩
type OtherScreeningName == {x : Text | x ∉ {"HADS", "PHQ-9", "GAD-7"}}
value SubscaleScore { subscale : Subscale; score : ℕ }     -- unit: score points
enum Subscale ::= wholeScale | anxietySubscale | depressionSubscale
fun screeningName : ScreeningInstrument → Text
axiom table SD-SC
axiom ∀ x : OtherScreeningName • screeningName(otherScreeningInstrument(x)) = x
fun screeningMax : ScreeningInstrument × Subscale ⇸ ℕ      -- the highest score of the subscale; unit: score points
axiom table SD-SR
```
- Meaning: The result of a depression or anxiety screening instrument (for example HADS, PHQ-9, GAD-7): instrument name, date and score, shown next to the headache outputs as a screening result, not as a psychiatric diagnosis.
- Conformance: Availability: SHOULD (INV-083) — R-MCF (4). Definitional: INV-085, INV-123. Labels and caveats: C3-10. Prohibited: C2-09.
- Realises: OUT-033, OUT-038
- Evidence: Stage 1 OUT-033. Score ranges, not stated in Stage 1: [S-104] E-059/Q01, [S-105] E-059/Q02, [S-105] E-059/Q03.
- Notes: Relations: INV-085, INV-123. R-MCF (4). Rationale: E-059/D01.

### 5.9 Special populations and classification support

### E-060 MenstrualRelationView and CycleLine
- Definition:
```omn
element MenstrualRelationView extends View {
  cycles : seq1 →CycleLine  core               -- the lines of the view, earliest first: consecutive menstrual cycles, preceded by a
                                               --   lead-in when the view shows no first day of menstruation on or before the first day of its period
  completeCycles : ℕ  derived MUST             -- the number of complete cycles the view covers
}
element CycleLine extends Item {
  cycle : DateSpan  core                        -- from the first day of menstruation (day 1) or, for a lead-in, from the first day of the
                                                --   period the view covers; to the day before the next first day of menstruation or, for a
                                                --   line that has not ended, to the last day of the period the view covers
  dayOneShown : 𝔹  core                         -- the line begins on a first day of menstruation that it shows; false for a lead-in
  complete : 𝔹  core                            -- the line has ended: it is shown to the day before the next first day of menstruation
  menstruationDays : set Date  MUST             -- the days of menstruation of the line; not empty when its day 1 is shown
  firstDayOfMenstruation : opt Date  derived MUST when self.dayOneShown    -- day 1
  perimenstrualWindow : opt DateSpan  derived MUST when self.dayOneShown   -- ICHD-3 appendix A1.1: day 1 ± 2 (days −2 to +3)
  nextWindowDays : opt DateSpan  derived MUST when self.complete           -- the days of the line in the perimenstrual window of
                                                                           --   the next menstruation (its days −2 and −1)
  migraineDays : set Date  MUST                 -- the migraine days of the line
  attacks : set →AttackMark  MUST  shown         -- the migraine attacks of the line
}
-- windowDaysBefore, windowDaysAfter: table SD-FX
-- shownDayOnes(cl): the first days of menstruation that the line shows: its day 1, and, for a line that has ended, the first day of
-- the next menstruation, the day after its last day (INV-124)
fun shownDayOnes(cl : CycleLine) : set Date ≙ cl.firstDayOfMenstruation ∪ {d : Date | cl.complete ∧ d = next(cl.cycle.to)}
```
- Meaning: For patients who menstruate, migraine attacks and migraine days in relation to the days of menstruation across consecutive cycles, with the perimenstrual window of ICHD-3 appendix A1.1 distinguished from the other days of the cycle, and the number of complete cycles the view covers. A line whose first day of menstruation is not shown (`dayOneShown` false) is a *lead-in*: the days from the first day of the covered period to the day before the earliest first day of menstruation the view shows, or to the end of the covered period when the view shows none. A lead-in is shown when no first day of menstruation on or before the first day of the covered period is known from the summarised diary information, for example when an adolescent's first menstruation (menarche) falls within the covered period, or when the diary information gives no first day for the menstruation in progress on that day. No first day of menstruation that the diary information gives lies in a lead-in. A lead-in is not a menstrual cycle: it shows no day 1 and no window of its own, and it is never counted as a complete cycle.
- Conformance: Availability: MUST (INV-086); applicability: "For patients who menstruate", `menstruatesDuring(c, c.timeRange)`. Definitional: INV-087, INV-124. Placement: `attacks` (W2, definitional).
- Realises: OUT-030, OUT-035
- Evidence: Stage 1 OUT-030. The window, not stated in Stage 1: [S-001] E-060/Q01, [S-001] E-060/Q02.
- Notes: Relations: INV-087, INV-124. See ISS-03. Rationale: E-060/D01, E-060/D02, E-060/D03, E-060/N01.

### E-061 AttackMark
- Definition:
```omn
element AttackMark extends Item {
  onset : Date  core
  inPerimenstrualWindow : 𝔹  derived MUST
}
```
- Meaning: A migraine attack shown by its onset date as an attack of a cycle line (a menstrual cycle or a lead-in, E-060) shown in the same view (in the menstrual-relation view or the patient-facing overview), marked as inside or outside the perimenstrual window of the menstruations that its line shows.
- Conformance: Content of E-060 (MUST). Definitional: INV-087.
- Realises: OUT-030
- Evidence: Stage 1 OUT-030.
- Notes: Relations: INV-087. See ISS-03. Rationale: E-061/D01, E-061/D02.

### E-062 ClusterView
- Definition:
```omn
element ClusterView extends View {
  bouts : seq →ClusterPeriodItem  SHOULD          -- cluster periods (bouts), earliest first, including previous bouts
  remissions : seq →RemissionPeriodItem  SHOULD   -- cluster remission periods, earliest first
  rates : set →ClusterAttackRate  SHOULD          -- attacks per day and per week during active periods
  acute : set →AcuteTreatmentSummary  SHOULD when ctx.subject.acuteMedications ≠ ∅   -- effectiveness at 15 minutes and need for rescue treatment
}
```
- Meaning: For patients with cluster headache: cluster periods (bouts) and cluster remission periods with start dates, end dates and durations, using the ICHD-3 definitions; attacks per day and per week during active periods; the effectiveness of acute treatments at 15 minutes and the need for rescue treatment; and the history of previous bouts.
- Conformance: Availability: SHOULD (INV-088); applicability: "For patients with cluster headache", `hasType(c, c3_1)`.
- Realises: OUT-031
- Evidence: Stage 1 OUT-031.
- Notes: See ISS-12. Rationale: E-062/D01, E-062/X01.

### E-063 ClusterPeriodItem and RemissionPeriodItem
- Definition:
```omn
abstract element ClusterPhaseItem extends Item {
  start : opt Date  SHOULD
  end : opt Date  SHOULD when ¬ self.ongoing
  ongoing : 𝔹  core                                -- the period has not ended by the as-of date of the output
  duration : opt Duration  derived SHOULD
}
element ClusterPeriodItem extends ClusterPhaseItem { }
element RemissionPeriodItem extends ClusterPhaseItem { }
-- remissionMoreThanMonths: table SD-FX
fun lastDay(x : ClusterPhaseItem) : set Date ≙
  {d : Date | (x.ongoing ∧ d = ctx(outputOf(x)).asOf) ∨ (¬ x.ongoing ∧ d ∈ x.end)}   -- the end date, or the as-of date while ongoing
```
- Meaning: A cluster period ("the time during which cluster headache attacks occur regularly and at least once every other day", ICHD-3 Definitions of terms) or a cluster remission period (an attack-free period of more than three months, the duration that the ICHD-3 Definitions of terms require of a remission), shown with its start date, end date and duration. An ongoing period is one that has not ended by the as-of date of the output: it shows no end date, and its duration runs from its start to the as-of date (its duration to date). A period that has ended by the as-of date shows its end date, on or before the as-of date, and its duration from start to end.
- Conformance: Content of E-062 (SHOULD). Definitional: INV-089, INV-124.
- Realises: OUT-031
- Evidence: Stage 1 OUT-031 (definitions quoted from [S-001]). Not stated in Stage 1: [S-001] E-063/Q01.
- Notes: Relations: INV-089, INV-124. `ongoing` is needed so that the end-date obligation can be met for a period that has not ended by the as-of date, such as a current bout. See ISS-12. Rationale: E-063/D01, E-063/N01, E-063/W01.

### E-064 ClusterAttackRate
- Definition:
```omn
element ClusterAttackRate extends PeriodValue {
  basis : RateBasis  core
  rate : ℚ  derived core                           -- unit: attacks per day or attacks per week
  bout : →ClusterPeriodItem  core                  -- the active period the rate refers to
}
enum RateBasis ::= perDay | perWeek
```
- Meaning: The number of cluster headache attacks per day or per week during an active period (bout): the number of attacks of its type scope in its period divided by the length of the period in days (per day), or seven times that (per week), so that a rate over a period that is not one day or one week is an average per day or per week. Its type scope is of cluster headache only (`onlyOfType`, E-012).
- Conformance: Content of E-062: SHOULD (INV-088). Definitional: INV-089.
- Realises: OUT-031
- Evidence: Stage 1 OUT-031; [S-007] E-064/Q00, [S-007] E-064/Q01.
- Notes: Relations: INV-089. Rationale: E-064/D01, E-064/D02, E-064/D03.

### E-065 TriggerCooccurrenceView
- Definition:
```omn
element TriggerCooccurrenceView extends View {
  factor : TriggerFactor  core
  factorDates : set Date  core          -- days on which the potential trigger factor is shown as present
  attackOnsets : set Date  core         -- onset days of attacks
}
given TriggerFactor                     -- a potential trigger factor, as the output names it
```
- Meaning: The co-occurrence over time of attacks with a potential trigger factor, with the statements that it shows co-occurrence and not causation and that some apparent triggers are early (premonitory) symptoms of the attack.
- Conformance: Availability: MAY. Definitional: INV-110. Labels and caveats: C3-09.
- Realises: OUT-032, OUT-038
- Evidence: Stage 1 OUT-032.
- Notes: Relations: INV-110.

### 5.10 Audience-specific views

### E-066 ClinicianSummary
- Definition:
```omn
element ClinicianSummary extends View { }
pred summaryTimeCourse(v : View, sr : Series) ≙      -- the time course of the frequency measures over the periods of sr
  perPeriod(v, sr, HeadacheDays, allTypes) ∧ (hasType(ctx(outputOf(v)), c1) ⇒ perPeriod(v, sr, MigraineDays, allTypes)) ∧
  perPeriod(v, sr, ModerateSevereHeadacheDays, allTypes) ∧ perPeriod(v, sr, AttackCount, allTypes) ∧
  ∀ p ∈ ran sr.periods • 0 ∈ daysOf(v, migraineDays, p, allTypes) ⇒
    ∃ mk ∈ v.content ∩ MigraineFreePeriodMark • mk.period = p ∧ mk.typeScope = allTypes
```
- Meaning: A concise clinician-facing summary for the period since the previous consultation, or a period chosen by the clinician (any period up to the as-of date), that brings together the outputs most used in consultations: frequency measures and their time course (OUT-004 to OUT-009), acute-medication use and any medication-overuse indicator (OUT-014 to OUT-016), current and past treatments with response (OUT-018, OUT-023, OUT-024), instrument results (OUT-026), functional impact (OUT-027), completeness (OUT-003) and adherence (OUT-039). It can be shared with the treating clinician.
- Conformance: Availability: SHOULD (INV-094); applicability: clinician audiences. Content: SHOULD (INV-104).
- Realises: OUT-034, OUT-039
- Evidence: Stage 1 OUT-034, OUT-039.
- Notes: See ISS-04. R-MCF (3). Rationale: E-066/D01.

### E-067 PatientOverview
- Definition:
```omn
element PatientOverview extends View { }
-- courseOverlaps(c, t, p): the course of treatment t has started on or before the last day of p and has not stopped before the
-- first day of p, so that the treatment is taken during p
pred courseOverlaps(c : OutputContext, t : Treatment, p : Period) ≙
  (∃ s ∈ startOf(c, t) • s ≤ p.end) ∧ ¬ ∃ e ∈ c.subject.courseEvents • e.treatment = t ∧ e.kind is stop ∧ e.date < p.start
-- courseNotOutside(c, t, p): the context does not place the course of treatment t outside p: the course has not started after
-- the last day of p and has not stopped before the first day of p; a course whose start the context does not state counts as started
pred courseNotOutside(c : OutputContext, t : Treatment, p : Period) ≙
  (∀ s ∈ startOf(c, t) • s ≤ p.end) ∧ ¬ ∃ e ∈ c.subject.courseEvents • e.treatment = t ∧ e.kind is stop ∧ e.date < p.start
```
- Meaning: An understandable overview, in plain language, of the patient's own headache pattern over time: headache and migraine days, intensity, acute-medication use, treatment effect and, where relevant, the relationship to menstruation, so that patients can follow the effect of their treatment and prepare consultations. `courseOverlaps(c, t, p)` holds when the context states a start of the course of treatment t on or before the last day of the period p and the course has not stopped (or been paused) before its first day, so that the treatment is taken during p. `courseNotOutside(c, t, p)` holds when the context does not place the course of t outside p: the course has not started after the last day of p and has not stopped (or been paused) before its first day. It differs from `courseOverlaps` only for a course whose start the context does not state, which it counts as started; for a course with a stated start the two agree, because a course has at most one start (INV-001).
- Conformance: Availability: SHOULD (INV-095); applicability: patient, parent and caregiver audiences. Content: SHOULD (INV-105).
- Realises: OUT-035
- Evidence: Stage 1 OUT-035.
- Notes: See ISS-03. R-MCF (1), (2). Rationale: E-067/W01.

## 6. Invariants

### 6.0 Generic invariants

The invariants of this section state, once each, rules that v34 stated for each output separately (PROCESS.md section 6a). INV-118, INV-119, INV-120 and INV-125 are level-indexed (section 3.3, item 7): they read their cases, with the level of each, from a case table (C1, C2, C3 of section 4.4; SD-DF of section 11). The invariants they replace are listed in section 9.

### INV-118 Per-period values are available for every period of the selected time range
- Predicate:
```omn
∀ r : CatalogueRow • ppGranularities(r, l) ≠ ∅ ⇒
  ∃ g ∈ ppGranularities(r, l) • ∀ c ∈ Ctx • c.granularity = g ⇒ ∀ q ∈ ppRequired(r, l, c) • reportedTogether(c, q.2, q.1)
```
- Reading: For every catalogue row with a case at level l in table C1, there is a granularity among those that the case names such that, for every admissible context of that granularity and for every pair of a type scope and kinds of per-period value that the case asks for in that context (`ppRequired`), the diary can produce an output in which one view and one series that spans the selected time range show, for every period of the series, values of each of these kinds with that type scope (`reportedTogether`, section 3.4).
- Conformance: level-indexed (section 3.3, item 7): MUST for the cases of table C1 with `l = must` (C1-01, C1-02, C1-04, C1-06, C1-10, C1-13); SHOULD for those with `l = should` (C1-03, C1-05, C1-07, C1-08, C1-09, C1-11, C1-12, C1-14). Scope: repertoire.
- Realises: OUT-001, OUT-004, OUT-005, OUT-006, OUT-007, OUT-010, OUT-011, OUT-012, OUT-014, OUT-015, OUT-027, OUT-029
- Evidence: Stage 1 statement parts named in the Stage 1 part column of table C1.
- Notes: Each case has its own existential granularity: the two measures of C1-04 and C1-06, and the cases C1-07 and C1-14, are separate cases. Replaces INV-014 to INV-019, INV-022, INV-023, INV-025, INV-026, INV-028, INV-029 and INV-108 (section 9). Rationale: INV-118/D01, INV-118/D02, INV-118/D03.

### INV-119 No element is presented with a prohibited claim
- Predicate:
```omn
¬ ∃ x : Element; r : CatalogueRow; q ∈ prohibitedClaims(r, l) • x ∈ q.2 ∧ ∃ C ∈ q.1 • presents(x, C)
```
- Reading: For every pair of a set of claims and a set of bearers in a case of table C2 at level l, no element of the output among those bearers is presented with a claim of that set, by its own wording or by an annotation that qualifies it (`presents`, E-001).
- Conformance: level-indexed (section 3.3, item 7): SHOULD NOT for the cases of table C2 with `l = shouldNot` (C2-01, C2-02, C2-03, C2-06, C2-07, C2-08, C2-09); MUST NOT for those with `l = mustNot` (C2-04, C2-05). Scope: output.
- Realises: OUT-003, OUT-011, OUT-016, OUT-018, OUT-020, OUT-023, OUT-028, OUT-033, OUT-038
- Evidence: Stage 1 statement parts named in the Stage 1 part column of table C2.
- Notes: C2-08 and C2-09 are also implied by C2-01 at the same level; they are kept so that OUT-028 and OUT-033 trace to them. Replaces INV-013, INV-021, INV-043, INV-048, INV-065, INV-084, INV-101, INV-106 and INV-107 (section 9). Rationale: INV-119/D01, INV-119/D02, INV-119/D03, INV-119/D04.

### INV-120 Required labels and caveats are shown
- Predicate:
```omn
∀ x : Element; r : CatalogueRow; q ∈ requiredAnnotations(r, l) • x ∈ q.2 ⇒ annotated(x, q.1)
```
- Reading: For every pair of an annotation kind and a set of bearers in a case of table C3 at level l, every element of the output among those bearers is qualified by an annotation of that kind (`annotated`, E-010).
- Conformance: level-indexed (section 3.3, item 7): MUST for C3-04; SHOULD for C3-01, C3-03 and C3-05 to C3-12; the case C3-02 (`may`) imposes nothing. Scope: output.
- Realises: OUT-008, OUT-011, OUT-016, OUT-017, OUT-020, OUT-026, OUT-032, OUT-033, OUT-036, OUT-037, OUT-038
- Evidence: Stage 1 statement parts named in the Stage 1 part column of table C3. [S-014] INV-120/Q00.
- Notes: Replaces INV-020, INV-047, INV-052, INV-090, INV-098, INV-099, INV-100, and the annotation conjunct of INV-092 (section 9). Rationale: INV-120/D01, INV-120/D02, INV-120/D03, INV-120/S01.

### INV-121 Values within their period
- Predicate:
```omn
(∀ x : PeriodValue; n ∈ daysWithin(x) • n ≤ x.period.lengthDays) ∧
(∀ d : DurationSummary • d.kind = moderateSeverePainTime ∧ d.statistic = total ⇒ d.value ≤ daysLong(d.period.lengthDays))
```
- Reading: Every number of days that a per-period value shows within its period (`daysWithin`, E-012: a day count, the covered days of a completeness indicator, the days of a level of an intensity distribution, the days with an associated symptom, a caregiver's lost productive days) does not exceed the length of the period, and a total time with moderate/severe pain does not exceed the length of its period.
- Conformance: definitional (E-012, E-013, E-014, E-023, E-024, E-025, E-031). Scope: output.
- Realises: OUT-001, OUT-003, OUT-004, OUT-005, OUT-006, OUT-008, OUT-010, OUT-011, OUT-012, OUT-014, OUT-015, OUT-027, OUT-036
- Evidence: Stage 1 statements of the requirements listed.
- Notes: Replaces INV-005 and conjuncts of INV-012, INV-032 and INV-033 (section 9; plan section 5). Rationale: INV-121/D01.

### INV-122 Nested day counts do not exceed the counts that contain them
- Predicate:
```omn
(∀ v : View; p : Period; sc : TypeScope; k₁, k₂ : DayMeasure • nestedIn(k₁, k₂) ⇒
   ∀ a ∈ daysOf(v, k₁, p, sc); b ∈ daysOf(v, k₂, p, sc) • a ≤ b) ∧
(∀ v : View; p : Period; h : HeadacheType; k : DayMeasure •
   (k ∈ {headacheDays, migraineDays, moderateSevereHeadacheDays} ∨ k is acuteMedicationDays) ⇒
     ∀ a ∈ daysOf(v, k, p, ofType(h)); b ∈ daysOf(v, k, p, allTypes) • a ≤ b) ∧
(∀ v : View • ∀ e, f ∈ v.content ∩ EventCount • e.event = f.event ∧ sameSpan(e.period, spanOf(f.period)) ∧
   (∃ h : HeadacheType • e.typeScope = ofType(h)) ∧ f.typeScope = allTypes ⇒ e.count ≤ f.count)
```
- Reading: In one view, for periods with the same dates and the same type scope, a count of days with a property does not exceed the count of days with a property that contains it (`nestedIn`, E-014): moderate/severe headache days and headache days; symptom-free days and headache-free days; the days with a class and the days with any acute medication; the days with a drug and the days with its class; the days with a class of a set of classes and the days with any medication of the set; the days with any medication of a set of classes and the days with any acute medication; the days missed, impaired or severely impaired in a domain and the days affected in that domain. A value for one headache type does not exceed the value over all headache types combined, for headache days, migraine days, moderate/severe headache days and acute-medication days, and for an event count of a period with the same dates.
- Conformance: definitional (E-012, E-014, E-017, E-019, E-021, E-029, E-030). Scope: output.
- Realises: OUT-006, OUT-008, OUT-014, OUT-016, OUT-027, OUT-029, OUT-036
- Evidence: Stage 1 statements of the requirements listed; [S-002] INV-122/Q01.
- Notes: The last two conjuncts are the predicate of v34 INV-030. Replaces INV-030 and conjuncts of INV-024, INV-031 and INV-033 (section 9). Rationale: INV-122/D01, INV-122/D02.

### INV-123 Facts of the context that an output shows are facts the context states
- Predicate:
```omn
∀ x : Element; f ∈ factsShown(x) • stated(ctx, f)
```
- Reading: Every fact of the context that an element of the output shows (`factsShown`, E-001: a preventive or acute treatment course, a course event, a stop, a stopped course, a start of withdrawal, an acute medication used, use of medication of a scope by a day count above 0, an available instrument or screening result) is a fact that the context states (`stated`, E-008).
- Conformance: definitional (E-008, E-014, E-029, E-034, E-039, E-043, E-046, E-047, E-048, E-049, E-053, E-055, E-058, E-059). Scope: output.
- Realises: OUT-009, OUT-012, OUT-014, OUT-016, OUT-017, OUT-018, OUT-020, OUT-021, OUT-022, OUT-023, OUT-024, OUT-026, OUT-033, OUT-036, OUT-039
- Evidence: Stage 1 statements of the requirements listed; [S-012] INV-123/Q01.
- Notes: The class of this rule is every attribute whose value names an entity of the subject's profile, or presupposes an event of it; its members are the element kinds in `factsShown`. Three attributes of the class are tied by invariants that also do more: E-042 `treatment` and `anchorDate` (INV-058), E-056 (INV-080) and E-063 `end` (INV-089). Replaces INV-036, INV-113, INV-117 and conjuncts of INV-056, INV-067, INV-068, INV-075, INV-079, INV-082, INV-085 and INV-112 (section 9). R-MCF (1), (4). Rationale: INV-123/D01, INV-123/D02, INV-123/D03, INV-123/D04, INV-123/D05, INV-123/D06, INV-123/D07, INV-123/S01, INV-123/S02.

### INV-124 The dated phases that one output shows describe one history
- Predicate:
```omn
(∀ cl, cl₂ : CycleLine • ∀ d ∈ shownDayOnes(cl₂) • ¬ (cl.cycle.from < d ∧ d ≤ cl.cycle.to)) ∧
(∀ x, y : ClusterPhaseItem • (x ∈ RemissionPeriodItem ⇔ y ∈ RemissionPeriodItem) ⇒
   ∀ xs ∈ x.start; xe ∈ lastDay(x); ys ∈ y.start; ye ∈ lastDay(y) • (xs = ys ∧ xe = ye) ∨ xe < ys ∨ ye < xs) ∧
(∀ b : ClusterPeriodItem; r : RemissionPeriodItem • ∀ bs ∈ b.start; be ∈ lastDay(b); rs ∈ r.start; re ∈ lastDay(r) • be < rs ∨ re < bs)
```
- Reading: No cycle line of the output, in any of its views, spans a first day of menstruation that the output shows: neither the day 1 of a line nor the day after a line that has ended (`shownDayOnes`, E-060) lies after the first day of a line and on or before its last day. Two cluster periods, or two remission periods, that show their start date and last day have the same start date and last day or do not overlap, and a cluster period and a remission period that show them do not overlap.
- Conformance: definitional (E-060, E-063). Scope: output.
- Realises: OUT-030, OUT-031, OUT-035
- Evidence: Stage 1 OUT-030 (the perimenstrual window of ICHD-3 A1.1 [S-001]), OUT-035, OUT-031 ("using the ICHD-3 definitions" [S-001]); E-060/Q01, E-060/Q02, E-063/Q01.
- Notes: The third conjunct replaces the bout–remission conjunct of INV-089 for the whole output. Rationale: INV-124/D01.

### INV-125 Labels whose definition Stage 1 fixes
- Predicate:
```omn
∀ lb : DefinitionLabel • lb.measure ∈ dom fixedDefinition ∧ fixedDefinitionLevel(lb.measure) = l ⇒ lb.definition = fixedDefinition(lb.measure)
```
- Reading: A definition label for a measure whose definition Stage 1 fixes at level l (table SD-DF) names that definition: for headache days, ICHD-3 "headache days" (SD-DF-01, MUST); for attacks, ICHD-3 "frequency of attacks" (SD-DF-02, SHOULD).
- Conformance: level-indexed (section 3.3, item 7): MUST for SD-DF-01, SHOULD for SD-DF-02. Scope: output.
- Realises: OUT-004, OUT-007
- Evidence: Stage 1 OUT-004 ("with "headache days" as defined in ICHD-3 "Definitions of terms""), OUT-007 ("with "frequency of attacks" as defined in ICHD-3 "Definitions of terms"").
- Notes: Replaces INV-009 and INV-010 (section 9). Rationale: INV-125/D01.

### Placement markers (rule W2)

The attributes that carry a placement marker (section 2.5, rule W2). This list is an index of the declarations; the declarations govern.

| Element | Attribute | Marker |
|---|---|---|
| E-010 | `qualifies` | `shown` (definitional) |
| E-033 | `components` | `shown SHOULD when concerns(ctx, self.typeScope, c1)` |
| E-035 | `series`, `markers` | `shown SHOULD` |
| E-038 | `series` | `shown` (definitional) |
| E-039 | `series` | `shown SHOULD` |
| E-040 | `reference`, `compared` | `shown MUST when ofResponseComparison(self)` |
| E-043 | `timePoints` | `shown MUST` |
| E-046 | `comparison`, `residual`, `otherValues` | `shown SHOULD` |
| E-051 | `outcomes`, `sequence` | `shown SHOULD` |
| E-054 | `preventiveGroups`, `acuteGroups` | `shown SHOULD` |
| E-055 | `preventiveResponse`, `acuteResponse`, `adherence` | `shown SHOULD` |
| E-060 | `attacks` (`CycleLine`) | `shown` (definitional) |

Not marked: `ClassGroup.lines` (INV-078 places the lines in the history view), `MenstrualRelationView.cycles` (INV-087 states an equality), `ResidualBurden.change`, `migraineDays` and `moderateSevereHeadacheDays` (INV-060 places, for the residual burden it asks for next to a percentage change, the burden and its two day counts in the view of the change), the references of the cluster view (E-062/X01), and references to periods (INV-003).

### 6.1 Contexts and frame

### INV-001 Admissible contexts
- Predicate:
```omn
c.subject.headacheTypes ⊆ c.subject.possibleHeadacheTypes ∧
(∀ h, k ∈ c.subject.possibleHeadacheTypes • h ⊑ k ⇒ h = k) ∧
(hasType(c, c2) ∨ hasType(c, c3_1) ⇒ c.weeklyGranularityRelevant) ∧
c.timeRange.to ≤ c.asOf ∧
(∃ s : seq1 DateSpan • first(s).from = c.timeRange.from ∧ last(s).to = c.timeRange.to ∧
   (∀ i ∈ dom s • ofKind(s(i).from, s(i).to, c.granularity)) ∧ (∀ i ∈ dom s • i < #s ⇒ s(i + 1).from = next(s(i).to))) ∧
(∀ r ∈ ran c.comparedSpans • r.to ≤ c.asOf) ∧
(∀ d ∈ c.previousConsultation • d ≤ c.asOf) ∧ (∀ r ∈ c.chosenPeriod • r.to ≤ c.asOf) ∧
c.subject.preventiveTreatments ∩ c.subject.acuteTreatments = ∅ ∧
(∀ p ∈ c.subject.preventiveTypes • p.1 ∈ c.subject.preventiveTreatments) ∧
(∀ t ∈ c.subject.preventiveTreatments • ∃ ty : PreventiveTreatmentType • (t, ty) ∈ c.subject.preventiveTypes) ∧
(∀ p ∈ c.subject.preventiveFor • p.1 ∈ c.subject.preventiveTreatments ∧ p.2 ∈ c.subject.possibleHeadacheTypes) ∧
(∀ t ∈ c.subject.preventiveTreatments • ∃ h : HeadacheType • (t, h) ∈ c.subject.preventiveFor) ∧
c.subject.ihsQ6ChronicAlternative ⊆ c.subject.preventiveTreatments ∧
c.subject.aged12From ≤ c.subject.adultFrom ∧ (∀ s ∈ c.subject.menstruationSpans • s.to ≤ c.asOf) ∧
(∀ e ∈ c.subject.courseEvents • e.treatment ∈ c.subject.preventiveTreatments ∪ c.subject.acuteTreatments ∧ e.date ≤ c.asOf) ∧
(∀ t ∈ c.subject.preventiveTreatments ∪ c.subject.acuteTreatments • #{e ∈ c.subject.courseEvents | e.treatment = t ∧ e.kind = start} ≤ 1 ∧
   #{e ∈ c.subject.courseEvents | e.treatment = t ∧ e.kind is stop} ≤ 1) ∧
(∀ e ∈ c.subject.courseEvents; s ∈ startOf(c, e.treatment) • s ≤ e.date) ∧
(∀ e, f ∈ c.subject.courseEvents • e.treatment = f.treatment ∧ f.kind is stop ∧ (e.kind is doseChange ∨ e.kind = targetDoseReached) ⇒
   e.date ≤ f.date) ∧
(∀ p ∈ c.subject.resumes • p.1 ∈ c.subject.preventiveTreatments ∧ p.2 ∈ c.subject.preventiveTreatments ∧ drugOf(p.1) = drugOf(p.2) ∧
   ∃ e ∈ c.subject.courseEvents; s ∈ startOf(c, p.2) • e.treatment = p.1 ∧ e.kind is stop ∧ e.date < s) ∧
(∀ p, q ∈ c.subject.resumes • p.1 = q.1 ∨ p.2 = q.2 ⇒ p = q) ∧
(∀ m ∈ c.subject.acuteMedications • m.drug ∈ dom classOf) ∧
(∀ t ∈ c.subject.acuteTreatments • ∃ m ∈ c.subject.acuteMedications • m.drug = drugOf(t)) ∧
(∀ m ∈ c.subject.acuteMedications • ∃ t ∈ c.subject.acuteTreatments • drugOf(t) = m.drug) ∧
(∀ d ∈ c.subject.withdrawalStart • d ≤ c.asOf) ∧
(∀ a ∈ c.subject.instrumentAdministrations • a.date ≤ c.asOf) ∧ (∀ a ∈ c.subject.screeningAdministrations • a.date ≤ c.asOf)
```
- Reading: The headache types the subject has or has had are among those it has or may have, or has had or may have had, and no listed type is a subtype of another; for a subject who has or has had tension-type or cluster headache, weekly granularity is clinically relevant; the selected time range ends no later than the as-of date and consists of whole periods of the selected granularity; selected comparison periods, the previous consultation, a period chosen by the clinician (which need not consist of whole periods), treatment course events, the starts of withdrawal, the spans during which the subject menstruates and the available instrument and screening results lie on or before the as-of date; course events are events of the subject's treatments, and a treatment is either preventive or acute and has at most one start and at most one stop or pause; none of its other course events (dose changes, the date the target or tolerated dose was reached, the end of a treatment cycle, a stop or pause) precedes its start, and none of its dose changes, nor the date the target or tolerated dose was reached, follows its stop or pause; a course that resumes the treatment of another course (`resumes`) and the course it resumes are preventive courses of the same drug, the resumed course has its stop or pause dated before the start of the course that resumes it, and each course resumes at most one course and is resumed by at most one; guidance types, and the headache types a treatment is given for, are stated for preventive treatments only; every preventive treatment has at least one guidance type (`otherPreventive` when no other type describes it); every preventive treatment is given for at least one headache type, and only for headache types, that the subject has or may have, or has had or may have had; the IHS Q6 situation is stated for preventive treatments only; the subject's twelfth birthday is not after the first day on which it is an adult; every acute medication belongs to an ICHD-3 8.2 class; and the acute treatment courses and the acute medications describe the same history: the drug of every acute treatment course is the drug of an acute medication the subject has used, and the drug of every acute medication is the drug of an acute treatment course.
- Conformance: definitional (characterises `Ctx`, section 3.2). Scope: context.
- Realises: OUT-001, OUT-004, OUT-009, OUT-014, OUT-018, OUT-022, OUT-024, OUT-029, OUT-034
- Evidence: Stage 1 OUT-001, OUT-004, OUT-009, OUT-014, OUT-034, OUT-018, OUT-022, OUT-024, OUT-029; [S-011], [S-013], [S-015] INV-001/Q00.
- Notes: Rationale: INV-001/D01, INV-001/D02, INV-001/D03.

### INV-002 Period length and kind agree with the dates
- Predicate:
```omn
∀ p : Period • p.start ≤ p.end ∧ p.lengthDays = days(p.start, p.end) ∧ ofKind(p.start, p.end, p.kind)
```
- Reading: A period does not end before it starts, its stated length is the number of its days, and a calendar month, 28-day period or calendar week has the dates of its kind.
- Conformance: definitional (E-005). Scope: output.
- Realises: OUT-001
- Evidence: Stage 1 OUT-001.

### INV-003 Every view states its period, and every period it uses is shown in it
- Predicate:
```omn
∀ v : View • v.covers ∈ v.content ∧ refs(v) ∩ Period ⊆ v.content ∧ ∀ x ∈ v.content • refs(x) ∩ Period ⊆ v.content ∧
  ∀ m ∈ referencedValues(x) • ∃ p ∈ v.content ∩ Period • sameSpan(p, spanOf(m.period))
```
- Reading: The reporting period a view covers is shown in the view, and every period that the view or one of its items refers to (the period of a measure, the periods of a series or a comparison, a window or span) is shown, with its dates and length, in the same view. A view that shows a change, a residual burden or a composite index also shows, with their dates and length, the periods of the values it refers to (`referencedValues`, E-011), wherever those values are shown.
- Conformance: MUST. Scope: output.
- Realises: OUT-001
- Evidence: Stage 1 OUT-001 ("Every summary output MUST state the reporting period it covers (start date, end date and length)").
- Notes: **Items that refer to the same period atom are in one view.** A period is an item, and every item is part of exactly one view (section 2.5). By INV-003, a period that an item refers to is part of that item's view. So if two items x and y refer to the same period atom p, then viewOf(x) = viewOf(p) = viewOf(y): in every output that satisfies INV-003, `∀ x, y : Item; p : Period • p ∈ refs(x) ∩ refs(y) ⇒ viewOf(x) = viewOf(y)`. Rationale: INV-003/D01, INV-003/D02, INV-003/S01.

### INV-004 A series consists of consecutive periods of its granularity
- Predicate:
```omn
∀ sr : Series • consecutive(sr.periods) ∧ ∀ p ∈ ran sr.periods • p.kind = sr.granularity
```
- Reading: Each period of a series begins on the day after the previous one ends, and all periods have the series granularity.
- Conformance: definitional (E-006). Scope: output.
- Realises: OUT-001, OUT-004, OUT-009
- Evidence: Stage 1 OUT-004 ("shown for every period in the selected time range"), OUT-009 ("a time series of consecutive reporting periods").

### INV-006 One value per measure, period and scope in a view
- Predicate:
```omn
(∀ v : View • ∀ m, n ∈ v.content ∩ DayCount • m.measure = n.measure ∧ m.typeScope = n.typeScope ∧ sameSpan(m.period, spanOf(n.period)) ⇒
   m.days = n.days ∧ (m.period = n.period ⇒ m = n)) ∧
(∀ v : View • ∀ m, n ∈ v.content ∩ EventCount • m.event = n.event ∧ m.typeScope = n.typeScope ∧ sameSpan(m.period, spanOf(n.period)) ⇒
   m.count = n.count ∧ (m.period = n.period ⇒ m = n))
```
- Reading: A view does not show two different values of the same count for the same period and type scope: two counts of the same measure, or of the same event, and type scope whose periods have the same start and end dates show the same number, whichever period atom each refers to, and a count of one period atom is shown once.
- Conformance: definitional (E-014, E-019). Scope: output.
- Realises: OUT-004, OUT-007
- Evidence: Stage 1 OUT-004, OUT-007.
- Notes: Rationale: INV-006/D01, INV-006/S01.

### 6.2 Definition labels and completeness

### INV-008 Definition labels for the defined measures
- Predicate:
```omn
∀ v : View; lm : LabelledMeasure • reports(v, lm) ⇒ ∃ l ∈ v.content ∩ DefinitionLabel • l.measure = lm
```
- Reading: A view that reports migraine days, headache days, moderate/severe headache days or attacks, in any form the model shows them, states which published definition of each it follows. The forms are: a per-period value of the measure, shown in the view or referred to by a change, a residual burden or a composite index shown in it; a distribution of headache days by peak intensity (headache days); the mark of a period without migraine days (migraine days); cycle lines, with the migraine days and the migraine attacks of each cycle (migraine days and attacks); cluster attack rates (attacks); and the attack onsets of a trigger co-occurrence view (attacks).
- Conformance: SHOULD. Scope: output.
- Realises: OUT-002, OUT-005, OUT-006, OUT-007, OUT-028
- Evidence: Stage 1 OUT-002 ("Outputs that report migraine days, headache days, moderate/severe headache days or attacks SHOULD state which published definition of each measure they follow"; Rationale: "different definitions give different numbers"), OUT-005 (label SHOULD), OUT-006 ("with the definition named as in OUT-002"), OUT-007, OUT-028; the outputs that report these measures in other forms: OUT-008 ("periods without migraine days"), OUT-010 ("the distribution of headache days by peak intensity category"), OUT-018 and OUT-019 (changes and residual burden), OUT-030 ("show migraine attacks and migraine days in relation to the days of menstruation"), OUT-031 ("attacks per day and per week during active periods"), OUT-032 ("the co-occurrence over time of attacks with potential trigger factors") and OUT-037 (the component measures of an index).
- Notes: The label is an item of the view, not of the element that reports the measure, so the elements themselves are unchanged. Because the labels of one view for one measure name one definition (INV-111, definitional), a view that meets this invariant states exactly one definition for each measure it reports (`labelledAs`, E-011), so the definition each shown value follows is stated (OUT-002). Rationale: INV-008/S01.

### INV-111 One definition per measure in a view
- Predicate:
```omn
(∀ v : View; l₁, l₂ ∈ v.content ∩ DefinitionLabel • l₁.measure = l₂.measure ⇒ l₁.definition = l₂.definition) ∧
(∀ v : View; x ∈ v.content; m ∈ referencedValues(x); lm : LabelledMeasure • isMeasure(m, lm) ⇒
   ∀ l₁ ∈ v.content ∩ DefinitionLabel; l₂ ∈ viewOf(m).content ∩ DefinitionLabel • l₁.measure = lm ∧ l₂.measure = lm ⇒
     l₁.definition = l₂.definition) ∧
(∀ v : View; x ∈ v.content; m₁, m₂ ∈ referencedValues(x); lm : LabelledMeasure • isMeasure(m₁, lm) ∧ isMeasure(m₂, lm) ⇒
   ∀ l₁ ∈ viewOf(m₁).content ∩ DefinitionLabel; l₂ ∈ viewOf(m₂).content ∩ DefinitionLabel • l₁.measure = lm ∧ l₂.measure = lm ⇒
     l₁.definition = l₂.definition)
```
- Reading: A view follows one published definition for each measure whose definition it states: all the definition labels it shows for migraine days, headache days, moderate/severe headache days or attacks name the same definition for that measure. A view that shows a change, a residual burden or a composite index whose values of such a measure are shown in another view states, where both views state a definition for the measure, the same definition as that view, the one those values follow. The values that one change, residual burden or composite index refers to come from views that, where both state a definition for the measure, state the same one.
- Conformance: definitional (E-011). Scope: output.
- Realises: OUT-002
- Evidence: Stage 1 OUT-002 ("Outputs that report migraine days, headache days, moderate/severe headache days or attacks SHOULD state which published definition of each measure they follow"; Rationale: "There is no single universally adopted definition of a migraine day; different definitions give different numbers. A reader can compare a diary value with guideline or trial values only if the definition used is visible.").
- Notes: Rationale: INV-111/D01, INV-111/D02, INV-111/S01.

### INV-011 A completeness indicator accompanies each reporting period
- Predicate:
```omn
∀ v : View •
  (∀ m ∈ v.content ∩ PeriodValue • m ∉ CompletenessIndicator ⇒ ∃ ci ∈ v.content ∩ CompletenessIndicator • ci.period = m.period) ∧
  (∀ x ∈ v.content; m ∈ referencedValues(x) • ∃ ci ∈ v.content ∩ CompletenessIndicator • sameSpan(ci.period, spanOf(m.period))) ∧
  (∀ a ∈ v.content ∩ AdherenceSummary • ∃ ci ∈ v.content ∩ CompletenessIndicator • ci.period = a.window) ∧
  (v ∈ TriggerCooccurrenceView ∨ v.content ∩ CycleLine ≠ ∅ ∨ v.content ∩ ClusterPhaseItem ≠ ∅ ⇒
     ∃ ci ∈ v.content ∩ CompletenessIndicator • ci.period = v.covers)
```
- Reading: For every reporting period for which a view shows a summary measure, the same view shows how completely the period is covered by diary information, as a number of covered days, a proportion or another expression, alone or together. These periods are the period of every per-period value shown; the period of each value that a change, a residual burden or a composite index shown in the view refers to, wherever that value is shown (by a period with its dates in the view); the window of every adherence summary shown; and the covered period of a view that shows cycle lines (migraine days and attacks in relation to menstruation), cluster periods or remission periods, or is a trigger co-occurrence view, whose summaries concern the diary information of that period (the dates a trigger co-occurrence view shows lie in it, INV-110).
- Conformance: SHOULD. Scope: output.
- Realises: OUT-003, OUT-034
- Evidence: Stage 1 OUT-003 ("Each reporting period SHOULD be accompanied by an indicator of how completely the period is covered by diary information [...], shown next to the summary measures"; Rationale: "Missing diary days bias frequency measures"), OUT-034 (completeness in the clinician-facing summary); the summaries that are not per-period values: OUT-018 and OUT-019 (changes and residual burden), OUT-030, OUT-031 (bouts and remissions), OUT-032, OUT-037 (component measures) and OUT-039 ("patient-reported adherence to the prescribed preventive regimen over the evaluation window").
- Notes: Rationale: INV-011/D01, INV-011/S01.

### INV-012 Completeness values agree with the period
- Predicate:
```omn
∀ ci : CompletenessIndicator • ci.typeScope = allTypes ∧
  (∀ e₁, e₂ ∈ ci.expressions • (e₁ is coveredDays ∧ e₂ is coveredDays) ∨ (e₁ is proportionCovered ∧ e₂ is proportionCovered) ⇒ e₁ = e₂) ∧
  (∀ n : ℕ; q : Percent • coveredDays(n) ∈ ci.expressions ∧ proportionCovered(q) ∈ ci.expressions ⇒ q ≈ 100 × n ÷ ci.period.lengthDays) ∧
  (∀ cj ∈ viewOf(ci).content ∩ CompletenessIndicator • sameSpan(cj.period, spanOf(ci.period)) ⇒
     ∃ n : ℕ • ∀ e ∈ ci.expressions ∪ cj.expressions •
       (∀ k : ℕ • e = coveredDays(k) ⇒ k = n) ∧ (∀ q : Percent • e = proportionCovered(q) ⇒ q ≈ 100 × n ÷ ci.period.lengthDays))
```
- Reading: Completeness is stated for all headache types combined, and is expressed at most once as covered days and at most once as a proportion; a proportion shown with the covered days is the covered days divided by the period length, in per cent. Two indicators that one view shows for periods with the same dates rest on one number of covered days: the covered days that each states are that number, and each proportion is that number divided by the period length, in per cent.
- Conformance: definitional (E-013). Scope: output.
- Realises: OUT-003
- Evidence: Stage 1 OUT-003 ("expressed as the proportion of days of the period that the diary covers").
- Notes: Rationale: INV-012/D01, INV-012/S01.

### 6.3 Frequency, severity and other per-period values

### INV-024 Totals, classes and drugs agree with sums
- Predicate:
```omn
∀ v : View; p : Period; sc : TypeScope •
  (∀ ks : set1 AcuteDrugClass; u ∈ daysOf(v, acuteMedicationDays(ofClasses(ks)), p, sc) •
     ((∀ k ∈ ks • daysOf(v, acuteMedicationDays(ofClass(k)), p, sc) ≠ ∅) ⇒
        u ≤ Σ k ∈ ks • Σ n ∈ daysOf(v, acuteMedicationDays(ofClass(k)), p, sc) • n)) ∧
  (let K == {m ∈ ctx.subject.acuteMedications • classOf(m.drug)} •
     (∀ k ∈ K • daysOf(v, acuteMedicationDays(ofClass(k)), p, sc) ≠ ∅) ⇒
       ∀ t ∈ daysOf(v, acuteMedicationDays(allAcuteMedication), p, sc) •
         t ≤ Σ k ∈ K • Σ n ∈ daysOf(v, acuteMedicationDays(ofClass(k)), p, sc) • n) ∧
  (∀ k : AcuteDrugClass • let D == {m ∈ ctx.subject.acuteMedications | classOf(m.drug) = k • m.drug} •
     D ≠ ∅ ∧ (∀ dr ∈ D • daysOf(v, acuteMedicationDays(ofDrug(dr)), p, sc) ≠ ∅) ⇒
       ∀ n ∈ daysOf(v, acuteMedicationDays(ofClass(k)), p, sc) •
         n ≤ Σ dr ∈ D • Σ x ∈ daysOf(v, acuteMedicationDays(ofDrug(dr)), p, sc) • x)
```
- Reading: In one view, for the same period (periods with the same dates, `daysOf`, E-014) and type scope: when every class of a set of classes (the 8.2.6 basis) is shown, the days with any medication of the set do not exceed the sum of the class values; when every class of the subject's acute medications (every acute medication it has used up to the as-of date, E-008) is shown, the total does not exceed the sum of the class values; and when every drug of a class that the subject has used up to the as-of date is shown, the class value does not exceed the sum of the drug values.
- Conformance: definitional (E-029). Scope: output.
- Realises: OUT-014, OUT-016
- Evidence: Stage 1 OUT-014 ("broken down by drug class [...] and by individual drug, together with the total across classes"), OUT-016.

### INV-027 Functional impact compared with the baseline period
- Predicate:
```omn
∀ c ∈ Ctx; t ∈ c.subject.preventiveTreatments • startOf(c, t) ≠ ∅ ⇒
  ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views; rc ∈ v.content ∩ ResponseComparison • rc.treatment = t ∧
    ∃ sd : ImpactDomain • ∀ p ∈ {rc.baseline} ∪ ran rc.onTreatment •
      (∀ d ∈ {paidWorkOrSchool, householdWork, socialOrLeisure} • ∃ m ∈ v.content ∩ fiDays(d, affected) • m.period = p ∧ m.typeScope = allTypes) ∧
      (∃ m ∈ v.content ∩ fiDays(sd, severelyImpaired) • m.period = p ∧ m.typeScope = allTypes)
```
- Reading: For each preventive treatment whose start the context states, functional impact can be shown for the pre-treatment baseline period and the on-treatment periods, next to the response comparison: for each of these periods, the days on which headache affected paid work or school, household work and social or leisure activities, and the days with severe functional impairment, counted in one domain for all of these periods (for example any activity), so that they can be compared with the baseline period.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-027
- Evidence: Stage 1 OUT-027 ("including days with severe functional impairment, expressed in days per period, and SHOULD allow comparison with the baseline period").
- Notes: R-MCF (1). Rationale: INV-027/D01, INV-027/S01.

### INV-031 Relations between day measures
- Predicate:
```omn
∀ v : View; p : Period; sc : TypeScope •
  (∀ a ∈ daysOf(v, headacheFreeDays, p, sc); b ∈ daysOf(v, headacheDays, p, sc) • a + b ≤ p.lengthDays) ∧
  (labelledAs(v, migraineDaysMeasure, ihs2025MigraineDay) ⇒
     ∀ u ∈ daysOf(v, migraineOrModerateSevereHeadacheDays, p, sc); a ∈ daysOf(v, migraineDays, p, sc) • a ≤ u) ∧
  (∀ n ∈ daysOf(v, migraineDays, p, sc) •
     (∃ mk ∈ v.content ∩ MigraineFreePeriodMark • mk.period = p ∧ mk.typeScope = sc) ⇒ n = 0)
```
- Reading: In one view, for the same period (periods with the same dates, `daysOf`, E-014) and scope: headache-free days and headache days together do not exceed the period length; where the view states that its migraine days follow the definition of a migraine day of the IHS position statement 2025, the days with migraine or moderate-to-severe headache, which rest on that definition, are not fewer than the migraine days; a period marked as without migraine days shows no migraine days.
- Conformance: definitional (E-018, E-020, E-022). Scope: output.
- Realises: OUT-008, OUT-020
- Evidence: Stage 1 OUT-008, OUT-020, OUT-002; [S-010] INV-031/Q00.
- Notes: Relations: INV-122. Rationale: INV-031/D01, INV-031/X01.

### INV-032 Intensity values lie on their scale
- Predicate:
```omn
∀ i : IntensitySummary •
  (∀ s ∈ i.scale • (∀ j ∈ dom s.points • j < #s.points ⇒ s.points(j).score < s.points(j + 1).score) ∧
     (∀ ds : set1 LevelDays • i.summary = peakIntensityDistribution(ds) ⇒ ∀ ld ∈ ds • ld.level ∈ ran s.points) ∧
     (∀ q : ℚ • i.summary = meanPeakIntensity(q) ⇒ first(s.points).score ≤ q ∧ q ≤ last(s.points).score)) ∧
  (∀ ds : set1 LevelDays • i.summary = peakIntensityDistribution(ds) ⇒
     (∀ ld₁, ld₂ ∈ ds • ld₁.level = ld₂.level ⇒ ld₁ = ld₂) ∧
     (∀ h ∈ daysOf(viewOf(i), headacheDays, i.period, i.typeScope) • (Σ ld ∈ ds • ld.days) ≤ h))
```
- Reading: The points of a scale are in increasing order; a distribution uses levels of the stated scale, once each, and its counts together do not exceed the headache days shown for the same period and scope; a mean peak intensity lies within the scale.
- Conformance: definitional (E-023). Scope: output.
- Realises: OUT-010
- Evidence: Stage 1 OUT-010 ("the distribution of headache days by peak intensity category, or an average peak intensity on the scale used").

### INV-033 Attacks with an associated symptom do not exceed the attacks
- Predicate:
```omn
∀ a : AssociatedSymptomSummary • ∀ n : ℕ; e ∈ viewOf(a).content ∩ AttackCount • a.presence = attacksWithSymptom(n) ∧
  sameSpan(e.period, spanOf(a.period)) ∧ e.typeScope = a.typeScope ⇒ n ≤ e.count
```
- Reading: The attacks with an associated symptom do not exceed the attacks that the same view shows for a period with the same dates and the same scope.
- Conformance: definitional (E-025). Scope: output.
- Realises: OUT-012
- Evidence: Stage 1 statements of the requirements listed.

### 6.4 Time course, comparisons and the three-month pattern

### INV-034 Time-course view available
- Predicate:
```omn
(∃ g ∈ MonthlyKind • ∀ c ∈ Ctx • c.granularity = g ⇒
   ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ TimeCourseView • tiles(v.series, c.timeRange, c.granularity)) ∧
(∀ c ∈ Ctx • c.granularity = calendarWeek ∧ c.weeklyGranularityRelevant ⇒
   ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ TimeCourseView • tiles(v.series, c.timeRange, calendarWeek))
```
- Reading: A time course of consecutive months or 28-day periods is available for the selected time range, and weekly values are available where weekly granularity is clinically relevant.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-009
- Evidence: Stage 1 OUT-009.

### INV-035 Time-course content and treatment markers
- Predicate:
```omn
∀ v : TimeCourseView • v.covers.start = first(v.series.periods).start ∧ v.covers.end = last(v.series.periods).end ∧
  perPeriod(v, v.series, HeadacheDays, allTypes) ∧ (hasType(ctx, c1) ⇒ perPeriod(v, v.series, MigraineDays, allTypes)) ∧
  perPeriod(v, v.series, ModerateSevereHeadacheDays, allTypes) ∧ perPeriod(v, v.series, AttackCount, allTypes) ∧
  ∀ e ∈ ctx.subject.courseEvents • e.treatment ∈ ctx.subject.preventiveTreatments ∧ markedKind(e.kind) ∧
    v.covers.start ≤ e.date ∧ e.date ≤ v.covers.end ⇒
      ∃ mk ∈ v.markers • mk.treatment = e.treatment ∧ mk.event = e.kind ∧ mk.date = e.date
```
- Reading: A time-course view covers exactly the periods of its series; it shows headache days, migraine days (for patients with migraine), moderate/severe headache days and attacks for every period of its series; and it has a dated marker for every start, dose change and stop of a preventive treatment within the period it covers.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-009
- Evidence: Stage 1 OUT-009 ("frequency measures (OUT-004 to OUT-007) as a time series of consecutive reporting periods [...] with dated markers for the start, dose change and stop of preventive treatments"). Migraine days keep the OUT-005 condition (section 3.5, reference rule).
- Notes: Rationale: INV-035/D01.

### INV-037 Comparison of selected periods of equal length
- Predicate:
```omn
∀ c ∈ Ctx • #c.comparedSpans ≥ 2 ∧ (∀ r, s ∈ ran c.comparedSpans • days(r.from, r.to) = days(s.from, s.to)) ⇒
  ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views; pc ∈ v.content ∩ PeriodComparison • matchesSelection(pc, c) ∧
    ∀ p ∈ ran pc.periods •
      (∃ m ∈ pc.values ∩ HeadacheDays • m.period = p ∧ m.typeScope = allTypes) ∧
      (hasType(c, c1) ⇒ ∃ m ∈ pc.values ∩ MigraineDays • m.period = p ∧ m.typeScope = allTypes) ∧
      (provides(ModerateSevereHeadacheDays) ⇒ ∃ m ∈ pc.values ∩ ModerateSevereHeadacheDays • m.period = p ∧ m.typeScope = allTypes) ∧
      (provides(AttackCount) ⇒ ∃ m ∈ pc.values ∩ AttackCount • m.period = p ∧ m.typeScope = allTypes)
```
- Reading: For any selection of two or more periods of equal length (for example a baseline period and a later period of the same length), the diary can show, side by side for exactly those periods and over all headache types combined, headache days, migraine days (for patients with migraine), and moderate/severe headache days and attacks wherever the diary provides them.
- Conformance: MUST. Scope: repertoire.
- Realises: OUT-001
- Evidence: Stage 1 OUT-001 ("the output MUST allow comparison of periods of equal length").
- Notes: R-MCF (3).

### INV-038 Comparison values refer to the compared periods
- Predicate:
```omn
∀ pc : PeriodComparison • ∀ m ∈ pc.values • m.period ∈ ran pc.periods
```
- Reading: Every value of a comparison belongs to one of the compared periods.
- Conformance: definitional (E-037). Scope: output.
- Realises: OUT-001
- Evidence: Stage 1 OUT-001.

### INV-039 Intensity can be compared between periods
- Predicate:
```omn
∀ c ∈ Ctx • #c.comparedSpans ≥ 2 ∧
  ((∃ r ∈ ran c.comparedSpans • childOn(c, r.from)) ⇒ ∀ r, s ∈ ran c.comparedSpans • days(r.from, r.to) = days(s.from, s.to)) ⇒
  ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views; pc ∈ v.content ∩ PeriodComparison •
    matchesSelection(pc, c) ∧ ∃ i₁ ∈ pc.values ∩ IntensitySummary • ∀ p ∈ ran pc.periods •
      ∃ m ∈ pc.values ∩ IntensitySummary • m.period = p ∧ m.typeScope = allTypes ∧ m.scale ≠ ∅ ∧ onSameScale(m, i₁)
```
- Reading: Intensity summaries over all headache types combined, with their scale, can be compared between selected periods, the summaries of the compared periods being on one scale and in one form (`onSameScale`, E-023), so that a change between them can be read; where the subject is a child or adolescent on the first day of one of the selected periods, between selected periods of equal length.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-010
- Evidence: Stage 1 OUT-010, OUT-036, OUT-001; [S-030] INV-039/Q00.
- Notes: R-MCF (3). Rationale: INV-039/D01, INV-039/D02, INV-039/S01.

### INV-040 Three-month pattern view available
- Predicate:
```omn
∃ g ∈ MonthlyKind • ∀ c ∈ Ctx • ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ ThreeMonthPatternView •
  v.series.granularity = g ∧ perPeriod(v, v.series, HeadacheDays, allTypes) ∧ perPeriod(v, v.series, MigraineDays, allTypes)
```
- Reading: For every context, a view of headache days and migraine days for each of the most recent three consecutive calendar months, or 28-day periods, is available.
- Conformance: MUST. Scope: repertoire.
- Realises: OUT-028
- Evidence: Stage 1 OUT-028.

### INV-041 Structure of the three-month pattern view
- Predicate:
```omn
∀ v : ThreeMonthPatternView • #v.series.periods = 3 ∧ v.series.granularity ∈ MonthlyKind ∧
  mostRecent(v.series, ctx.asOf) ∧ v.covers.start = first(v.series.periods).start ∧ v.covers.end = last(v.series.periods).end
```
- Reading: The series of the view has three consecutive monthly periods, the most recent ones that end on or before the as-of date, and the view covers exactly those.
- Conformance: definitional (E-038). Scope: output.
- Realises: OUT-028
- Evidence: Stage 1 OUT-028.

### INV-042 Three-month view shows the definitions it refers to
- Predicate:
```omn
∀ v : ThreeMonthPatternView • (∃ l ∈ v.content ∩ DefinitionLabel • l.measure = headacheDaysMeasure) ∧
  (∃ l ∈ v.content ∩ DefinitionLabel • l.measure = migraineDaysMeasure) ∧ c1_3 ∈ v.referencedCodes ∧
  (mayHaveType(ctx, c2) ⇒ c2_3 ∈ v.referencedCodes)
```
- Reading: The view shows the definitions of headache days and migraine days it follows and names ICHD-3 code 1.3 Chronic migraine, and 2.3 Chronic tension-type headache where the subject has or may have tension-type headache.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-028
- Evidence: Stage 1 OUT-028 ("The view SHOULD show the source definitions it refers to (see OUT-002)").

### 6.5 Medication overuse and withdrawal

### INV-044 Medication-overuse indicator per period, per class and for combined use
- Predicate:
```omn
∃ g ∈ MonthlyKind • ∀ c ∈ Ctx • c.granularity = g ⇒ ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views; sr ∈ v.content ∩ Series •
  tiles(sr, c.timeRange, g) ∧ ∀ p ∈ ran sr.periods •
    ∀ s ∈ {m ∈ c.subject.acuteMedications • ofClassUse(classOf(m.drug))} ∪ {combinedUse} •
      ∃ i ∈ v.content ∩ MedicationOveruseIndicator • i.period = p ∧ i.scope = s
```
- Reading: For every calendar month or 28-day period of the selected time range, the output indicates, for each class of the subject's acute medications (every acute medication it has used up to the as-of date, including one it no longer uses, E-008) and for the combined use of ICHD-3 8.2.6, whether acute medication use reached the ICHD-3 level of regular use over the time span the code refers to.
- Conformance: MUST. Scope: repertoire.
- Realises: OUT-016
- Evidence: Stage 1 OUT-016.

### INV-045 Medication-overuse indicator agrees with its code, level, span and basis
- Predicate:
```omn
∀ i : MedicationOveruseIndicator •
  i.code = overuseCode(i.scope) ∧ i.referenceLevel = overuseLevel(i.scope) ∧
  i.period.kind ∈ MonthlyKind ∧ consecutive(i.span) ∧ (∀ p ∈ ran i.span • p.kind = i.period.kind) ∧ last(i.span) = i.period ∧
  plusMonths(first(i.span).start, overuseSpanMonths) ≤ last(i.span).end ∧
  (#i.span ≥ 2 ⇒ ¬ (plusMonths(i.span(2).start, overuseSpanMonths) ≤ last(i.span).end)) ∧
  #i.basis = #i.span ∧
  (∀ j ∈ dom i.span • i.basis(j).period = i.span(j) ∧ i.basis(j).measure = acuteMedicationDays(basisScope(i.scope)) ∧
     i.basis(j).typeScope = allTypes) ∧
  (∀ k : AcuteDrugClass • i.scope = ofClassUse(k) ⇒
     (i.status = levelReached ⇔ ∀ j ∈ dom i.basis • i.basis(j).days ≥ i.referenceLevel))
```
- Reading: The indicator names the ICHD-3 subtype of its scope and that subtype's reference level (15 days per month for non-opioid analgesics, 10 for the other classes and for combined use). Its time span is the shortest run of consecutive monthly periods ending with the indicated period that lasts more than three months, and for each period of the span it rests on the shown days with medication of its scope. For a class, the level is reached exactly when every period of the span has at least the reference level of days.
- Conformance: definitional (E-032). Scope: output.
- Realises: OUT-016
- Evidence: Stage 1 OUT-016; [S-001] 8.2, 8.2.1–8.2.5, 8.2.8 quoted in E-032.
- Notes: Rationale: INV-045/D01.

### INV-046 Combined use of ICHD-3 8.2.6
- Predicate:
```omn
∀ i : MedicationOveruseIndicator • i.scope = combinedUse ⇒
  (i.status = levelReached ⇒ (∀ j ∈ dom i.basis • i.basis(j).days ≥ i.referenceLevel) ∧
     (¬ ∃ i₂ : MedicationOveruseIndicator • sameIndicatedPeriod(i₂, i) ∧ i₂.status = levelReached ∧
         ∃ k ∈ classesOf821to825 • i₂.scope = ofClassUse(k)) ∧
     (∃ k₁, k₂ ∈ classesOf826 • k₁ ≠ k₂ ∧ ¬ classUseExcluded(i, k₁) ∧ ¬ classUseExcluded(i, k₂))) ∧
  ((∀ j ∈ dom i.basis • i.basis(j).days ≥ i.referenceLevel ∧
      (∃ k₁, k₂ ∈ classesOf826 • k₁ ≠ k₂ ∧ classShownUsed(i, k₁, j) ∧ classShownUsed(i, k₂, j))) ∧
   (∀ k ∈ classesOf821to825 • (∃ m ∈ ctx.subject.acuteMedications • classOf(m.drug) = k) ⇒
      ∃ i₂ : MedicationOveruseIndicator • sameIndicatedPeriod(i₂, i) ∧ i₂.scope = ofClassUse(k) ∧ i₂.status = levelNotReached)
   ⇒ i.status = levelReached) ∧
  (∀ i₂ : MedicationOveruseIndicator • sameIndicatedPeriod(i₂, i) ∧ i₂.scope = combinedUse ⇒ i₂.status = i.status)
```
- Reading: The combined-use indication is "reached" only if the days with any medication of the 8.2.6 classes reach 10 in every period of the span, no class of 8.2.1–8.2.5 reaches its own level for the same period, and at least two classes of 8.2.6 may have been used in the span: neither the context (the subject has used no medication of the class up to the as-of date) nor the class indicators of the same period (0 days with the class in every period of the span) exclude them. A subject who has used a single class of 8.2.6 up to the as-of date, or whose class indicators show only one of these classes in the span, is therefore shown as "not reached", as ICHD-3 requires for cumulative use within the single class of non-opioid analgesics. When the combined days reach the level in every period of the span, the class indicators of the same period show days with at least two classes of 8.2.6 in each of these periods, and every class of 8.2.1–8.2.5 that the subject has used up to the as-of date is shown as not reached, the combined indication is "reached". Between these two cases (for example when a second class shows days in only some periods of the span) the relation does not fix the status, because ICHD-3 does not state whether "any combination" must hold in every month of the span; the reader sees the basis and the class values. The class indicators "of the same period" are those that the same view shows for a period with the same dates and kind, whichever period atom they refer to, and two combined-use indicators that one view shows for the same period give the same indication.
- Conformance: definitional (E-032). Scope: output.
- Realises: OUT-016
- Evidence: Stage 1 OUT-016; [S-001] INV-046/Q00, [S-001] INV-046/Q01.
- Notes: Rationale: INV-046/D01, INV-046/S01.

### INV-049 Withdrawal follow-up view available
- Predicate:
```omn
∀ c ∈ Ctx; ws ∈ c.subject.withdrawalStart •
  (c.timeRange.from = ws ∧ c.timeRange.to < plusMonths(ws, followUpMonths) ⇒
     ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ WithdrawalFollowUpView • v.withdrawalStart = ws ∧
       sameSpan(v.covers, c.timeRange) ∧ ∃ sr ∈ v.series • tiles(sr, c.timeRange, c.granularity)) ∧
  (c.asOf < plusMonths(ws, followUpMonths) ⇒
     ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ WithdrawalFollowUpView • v.withdrawalStart = ws ∧
       v.covers.start = ws ∧ v.covers.end = c.asOf)
```
- Reading: For each start of withdrawal of overused medication of the subject (every start up to the as-of date, E-008), the follow-up view is available for every time range that starts at that start of withdrawal and ends within the following year (the days from the start of withdrawal to the day before the same date 12 months later, section 2.8); it covers that time range, with a series of the selected granularity that spans it. While the as-of date lies within that year, the follow-up view is also available from the start of withdrawal to the as-of date, whatever the number of days between them.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-017
- Evidence: Stage 1 OUT-017 ("SHOULD show headache days and acute medication days from the start of withdrawal onward, including the review window 4 to 8 weeks after the start of withdrawal").
- Notes: Rationale: INV-049/D01, INV-049/S01, INV-049/W01.

### INV-050 Withdrawal follow-up content
- Predicate:
```omn
∀ v : WithdrawalFollowUpView • v.covers.start = v.withdrawalStart ∧
  shownDay(v, headacheDays, v.covers, allTypes) ∧ shownDay(v, acuteMedicationDays(allAcuteMedication), v.covers, allTypes) ∧
  (∀ sr ∈ v.series • first(sr.periods).start = v.withdrawalStart ∧ fillsPeriod(sr, v.covers) ∧
     perPeriod(v, sr, HeadacheDays, allTypes) ∧ perPeriod(v, sr, TotalAcuteMedicationDays, allTypes))
```
- Reading: The view begins on its start of withdrawal and shows headache days and acute-medication days for the period it covers and, where it has a series, for every period of that series, which begins on the start of withdrawal and consists of all whole periods of its granularity within the covered period (`fillsPeriod`, E-006).
- Conformance: SHOULD. Scope: output.
- Realises: OUT-017
- Evidence: Stage 1 OUT-017 ("SHOULD show headache days and acute medication days from the start of withdrawal onward").
- Notes: Rationale: INV-050/D01, INV-050/D02, INV-050/S01.

### INV-051 The NICE CG150 1.3.48 review window
- Predicate:
```omn
∀ v : WithdrawalFollowUpView; w ∈ v.reviewWindow •
  w.start = plusDays(v.withdrawalStart, 7 × reviewWindowFromWeeks) ∧ w.end = plusDays(v.withdrawalStart, 7 × reviewWindowToWeeks)
```
- Reading: The review window begins 4 weeks and ends 8 weeks after the start of withdrawal.
- Conformance: definitional (E-039). Scope: output.
- Realises: OUT-017
- Evidence: Stage 1 OUT-017 ("the review window 4 to 8 weeks after the start of withdrawal named in NICE CG150 recommendation 1.3.48").

### 6.6 Preventive treatment response

### INV-053 Absolute and percentage change agree with the values they compare
- Predicate:
```omn
∀ ch : Change • ch.reference.measure = ch.compared.measure ∧ ch.reference.typeScope = ch.compared.typeScope ∧
  ¬ sameSpan(ch.reference.period, spanOf(ch.compared.period)) ∧ (ch.absolute ≠ ∅ ∨ ch.relative ≠ ∅) ∧
  (∀ a ∈ ch.absolute • a = ch.compared.days − ch.reference.days) ∧
  (∀ r ∈ ch.relative • (ch.reference.days > 0 ⇒ ∃ q : ℚ • r = percent(q) ∧ q ≈ 100 × (ch.compared.days − ch.reference.days) ÷ ch.reference.days) ∧
     (ch.reference.days = 0 ⇒ r = undefinedForZeroReference))
```
- Reading: A change compares two values of the same measure and scope for two different periods, periods with different dates, and shows its absolute form, its percentage form or both; the absolute change is the compared value minus the reference value, and the percentage change is that difference divided by the reference value, in per cent, or is shown as not defined when the reference value is 0.
- Conformance: definitional (E-040). Scope: output.
- Realises: OUT-018
- Evidence: Stage 1 OUT-018 ("the absolute and percentage change from baseline").

### INV-055 Response comparison for each preventive treatment, at the evaluation time points
- Predicate:
```omn
∀ c ∈ Ctx; t ∈ c.subject.preventiveTreatments •
  (startOf(c, t) ≠ ∅ ⇒ ∃ o : Output • (c, o) ∈ Rep ∧ ∃ x ∈ parts(o) ∩ ResponseComparison • x.treatment = t) ∧
  (∀ r ∈ evaluationRules; a ∈ anchorDates(c, t, r.anchor); s ∈ startOf(c, t) •
     applicable(c, t, r) ∧ intervalOnTreatment(c, t, a, r) ∧ shift(a, r.minOffset) ≤ c.asOf ∧ fitsMonthlyPeriod(s, a, r) ⇒
       ∃ o : Output • (c, o) ∈ Rep ∧ ∃ x ∈ parts(o) ∩ ResponseComparison • x.treatment = t ∧
         equalLengths({x.baseline} ∪ ran x.onTreatment) ∧
         ∃ tp ∈ x.timePoints; p ∈ ran x.onTreatment • tp.rule = r ∧ tp.anchorDate = a ∧ atTimePoint(p, tp) ∧
           notStoppedBefore(c, t, p.end))
```
- Reading: For each preventive treatment whose start the context states, a response comparison is available. For each evaluation time point of a rule that applies to the treatment (`applicable`, E-041), whose interval the course is taken through (`intervalOnTreatment`, E-042), that has been reached by the as-of date, and at which a calendar month or 28-day period beginning on or after the treatment start can end (`fitsMonthlyPeriod`, E-042), a comparison of periods of equal length is available whose on-treatment period ends at that time point (`atTimePoint`, E-042; section 2.8) and on or before every stop or pause of the course.
- Conformance: MUST. Scope: repertoire.
- Realises: OUT-001, OUT-018, OUT-036
- Evidence: Stage 1 OUT-018, OUT-001, OUT-036; [S-034] INV-055/Q00.
- Notes: See ISS-10. R-MCF (1). Rationale: INV-055/D01, INV-055/D02, INV-055/D03, INV-055/S01, INV-055/W01.

### INV-056 Response comparison content
- Predicate:
```omn
∀ rc : ResponseComparison • rc.baseline.kind ∈ MonthlyKind ∧ (∀ p ∈ ran rc.onTreatment • p.kind ∈ MonthlyKind) ∧
  rc.baseline.end < rc.treatmentStart ∧ (∀ p ∈ ran rc.onTreatment • rc.treatmentStart ≤ p.start) ∧
  (∀ i ∈ dom rc.onTreatment • i < #rc.onTreatment ⇒ rc.onTreatment(i).end < rc.onTreatment(i + 1).start) ∧
  (∀ m ∈ rc.values • m.period ∈ {rc.baseline} ∪ ran rc.onTreatment) ∧
  (∀ ch ∈ rc.changes • ch.reference.period = rc.baseline ∧ ch.compared.period ∈ ran rc.onTreatment ∧
     ch.reference ∈ rc.values ∧ ch.compared ∈ rc.values) ∧
  ∀ k ∈ {headacheDays, migraineDays} •
    (∀ p ∈ {rc.baseline} ∪ ran rc.onTreatment • ∃ m ∈ rc.values • m.measure = k ∧ m.period = p ∧ m.typeScope = allTypes) ∧
    (∀ p ∈ ran rc.onTreatment • ∃ ch ∈ rc.changes • ch.reference.measure = k ∧ ch.reference.period = rc.baseline ∧
       ch.compared.period = p ∧ ch.reference.typeScope = allTypes)
```
- Reading: The baseline of a response comparison is a calendar month or 28-day period that ends before its treatment start date, and its on-treatment periods are calendar months or 28-day periods that begin on or after that date, in order, each ending before the next begins. Every value it shows refers to its baseline or to one of its on-treatment periods. For the baseline and every on-treatment period it shows headache days and migraine days over all headache types combined, and for every on-treatment period the change of each from baseline. Every change it shows compares a value it shows for an on-treatment period with the value it shows for the baseline.
- Conformance: MUST. Scope: output.
- Realises: OUT-018
- Evidence: Stage 1 OUT-018 ("compare monthly migraine days and monthly headache days [...] in a pre-treatment baseline period with periods after treatment start"; "showing both the values of each period and the absolute and percentage change from baseline"); OUT-001 (the monthly periods: calendar months or 28-day periods).
- Notes: Rationale: INV-056/D01.

### INV-057 Moderate/severe headache days in the comparison, where reported
- Predicate:
```omn
∀ rc : ResponseComparison • provides(ModerateSevereHeadacheDays) ⇒
  (∀ p ∈ {rc.baseline} ∪ ran rc.onTreatment • ∃ m ∈ rc.values • m.measure = moderateSevereHeadacheDays ∧ m.period = p ∧ m.typeScope = allTypes) ∧
  (∀ p ∈ ran rc.onTreatment • ∃ ch ∈ rc.changes • ch.reference.measure = moderateSevereHeadacheDays ∧
     ch.reference.period = rc.baseline ∧ ch.compared.period = p ∧ ch.reference.typeScope = allTypes)
```
- Reading: Where the diary reports moderate/severe headache days, the response comparison also shows them, with their changes from baseline.
- Conformance: MUST. Scope: output.
- Realises: OUT-018
- Evidence: Stage 1 OUT-018 ("and, where reported, moderate/severe headache days").

### INV-058 Evaluation time points agree with their rule and anchor
- Predicate:
```omn
∀ tp : EvaluationTimePoint • tp.rule ∈ evaluationRules ∧ applicable(ctx, tp.treatment, tp.rule) ∧
  tp.anchorDate ∈ anchorDates(ctx, tp.treatment, tp.rule.anchor) ∧ intervalOnTreatment(ctx, tp.treatment, tp.anchorDate, tp.rule) ∧
  tp.earliest = shift(tp.anchorDate, tp.rule.minOffset) ∧
  (∀ x ∈ tp.rule.maxOffset • tp.latest = {shift(tp.anchorDate, x)}) ∧ (tp.rule.maxOffset = ∅ ⇒ tp.latest = ∅)
```
- Reading: A time point belongs to a guidance rule that applies to the treatment: the treatment is of a type the rule names and of no type the rule excludes, and is within the population of the rule's guidance (given for migraine or a subtype of it, to a subject who was, on the start of the treatment, of the ages the guidance covers); its anchor date is the treatment's start, the date the tolerated or target dose was reached, or the end of the stated treatment cycle; the course is taken through the interval from that anchor date: no stop or pause of it is dated before the last day of the interval, the day before the time point (for a window, before its first date) (`intervalOnTreatment`, E-042); its date (or window) is the anchor date shifted by the rule's offset(s).
- Conformance: definitional (E-042). Scope: output.
- Realises: OUT-018
- Evidence: Stage 1 OUT-018 (see E-041).
- Notes: R-MCF (1).

### INV-059 Evaluation time points shown with the comparison
- Predicate:
```omn
∀ rc : ResponseComparison • (∀ tp ∈ rc.timePoints • tp.treatment = rc.treatment) ∧
  ∀ r ∈ evaluationRules; a ∈ anchorDates(ctx, rc.treatment, r.anchor) •
    applicable(ctx, rc.treatment, r) ∧ intervalOnTreatment(ctx, rc.treatment, a, r) ⇒ ∃ tp ∈ rc.timePoints • tp.rule = r ∧ tp.anchorDate = a
```
- Reading: Every evaluation time point that a response comparison shows is one of its treatment, and the comparison shows the evaluation time points of all guidance rules that apply to the treatment (`applicable`, E-041: to its type, unless the rule is named for all preventive treatment and the treatment has a type to which the same guidance gives a later time point of its own, `excludes`; and within the population of the guidance, `inPopulation`), at each anchor date whose interval the course is taken through (`intervalOnTreatment`, E-042).
- Conformance: MUST. Scope: output.
- Realises: OUT-018
- Evidence: Stage 1 OUT-018.
- Notes: R-MCF (1).

### INV-060 Residual burden next to a percentage change
- Predicate:
```omn
∀ ch : Change • ch.reference.measure ∈ {migraineDays, headacheDays} ∧ (∃ r ∈ ch.relative • r is percent) ∧
  ch.compared.period.lengthDays ≥ shortestMonthlyDays ⇒
  ∃ rb ∈ viewOf(ch).content ∩ ResidualBurden • rb.change = ch ∧ rb.migraineDays ∈ viewOf(ch).content ∧
    rb.moderateSevereHeadacheDays ∈ viewOf(ch).content
```
- Reading: Wherever a percentage change in migraine or headache days is shown whose compared period has at least 28 days (`shortestMonthlyDays`), the absolute numbers of migraine days and moderate/severe headache days per month that remain on treatment are shown next to it (see ISS-13).
- Conformance: SHOULD. Scope: output.
- Realises: OUT-019
- Evidence: Stage 1 OUT-019.
- Notes: See ISS-03. Rationale: INV-060/D01, INV-060/D02.

### INV-061 Residual burden refers to a monthly on-treatment period
- Predicate:
```omn
∀ rb : ResidualBurden • rb.migraineDays.measure = migraineDays ∧ rb.moderateSevereHeadacheDays.measure = moderateSevereHeadacheDays ∧
  rb.migraineDays.typeScope = rb.change.compared.typeScope ∧ rb.moderateSevereHeadacheDays.typeScope = rb.change.compared.typeScope ∧
  ∀ m ∈ {rb.migraineDays, rb.moderateSevereHeadacheDays} • m.period.kind ∈ MonthlyKind ∧ within(m.period, rb.change.compared.period) ∧
    (rb.change.compared.period.kind ∈ MonthlyKind ⇒ m.period = rb.change.compared.period)
```
- Reading: The residual burden shows migraine days and moderate/severe headache days, with the scope of the change, for one calendar month or 28-day period: the compared on-treatment period itself when that is a calendar month or 28-day period (as in every response comparison, INV-056), and otherwise one such period within the compared period.
- Conformance: definitional (E-044). Scope: output.
- Realises: OUT-019
- Evidence: Stage 1 OUT-019 ("per month that remain on treatment").

### INV-062 A responder label shows its criterion and the values it rests on
- Predicate:
```omn
∀ L : ResponderLabel • L.criterion ≠ ∅ ∧
  (∃ rc ∈ L.comparison • ran L.evaluated ⊆ ran rc.onTreatment ∧
     ∀ ch ∈ rc.changes • ch.compared.period ∈ ran L.evaluated ∧ (∃ q ∈ ch.relative • q is percent) ∧ ch.reference.measure ∈ {migraineDays, headacheDays} ⇒
       ∃ rb ∈ L.residual • rb.change = ch) ∧
  (∀ K ∈ L.criterion; u ∈ K.alsoRestsOn • valueAvailable(ctx, u) ⇒
     (∀ ins : Instrument • u = instrumentResultOf(ins) ⇒ (∃ r ∈ L.otherValues ∩ InstrumentResult • r.instrument = ins) ∧
        ∀ rc ∈ L.comparison • rc.treatment = L.treatment ∧
          (∃ a ∈ ctx.subject.instrumentAdministrations • a.instrument = ins ∧ rc.treatmentStart < a.date ∧
             inPeriod(a.date, last(L.evaluated))) ⇒
            ∃ r ∈ L.otherValues ∩ InstrumentResult • r.instrument = ins ∧ evaluationResult(L, r)) ∧
     (u = acuteTreatmentEffectiveness ⇒ ∀ p ∈ ran L.evaluated; am ∈ ctx.subject.acuteMedications •
        ∃ s ∈ L.otherValues ∩ AcuteTreatmentSummary • s.period = p ∧ s.typeScope = allTypes ∧ summarisesMedication(s, am)) ∧
     (∀ k : PeriodValueKind • u = periodValuesOf(k) ⇒
        ∀ p ∈ ran L.evaluated ∪ {rc ∈ L.comparison • rc.baseline} •
          (k ≠ acuteTreatmentSummaries ⇒
             ∃ m ∈ L.otherValues ∩ PeriodValue • m.period = p ∧ m.typeScope = allTypes ∧ valueOfKind(m, k)) ∧
          (k = acuteTreatmentSummaries ⇒ ∀ am ∈ ctx.subject.acuteMedications •
             ∃ s ∈ L.otherValues ∩ AcuteTreatmentSummary • s.period = p ∧ s.typeScope = allTypes ∧ summarisesMedication(s, am))) ∧
     (∀ k : PeriodValueKind; h : HeadacheType • u = typeValuesOf((k, h)) ⇒
        ∀ p ∈ ran L.evaluated ∪ {rc ∈ L.comparison • rc.baseline} •
          (k ≠ acuteTreatmentSummaries ⇒
             ∃ m ∈ L.otherValues ∩ PeriodValue • m.period = p ∧ scopeFor(ctx, m.typeScope, h) ∧ valueOfKind(m, k)) ∧
          (k = acuteTreatmentSummaries ⇒ ∀ am ∈ ctx.subject.acuteMedications •
             ∃ s ∈ L.otherValues ∩ AcuteTreatmentSummary • s.period = p ∧ scopeFor(ctx, s.typeScope, h) ∧ summarisesMedication(s, am))) ∧
     (∀ t : Text • u = otherValueNamed(t) ⇒ ∃ x ∈ L.otherValues • showsValueNamed(x, t))) ∧
  (∀ K ∈ L.criterion; r : ReductionComponent; d ∈ r.measures; rc ∈ L.comparison •
     reductionFromBaseline(r) ∈ K.components ∧ conditionHolds(ctx, L.treatment, r.condition) ∧ rc.treatment = L.treatment ∧
     provides({m : DayCount | m.measure = d}) ⇒
       ∀ p ∈ ran L.evaluated • ∃ ch ∈ rc.changes • ch.reference.measure = d ∧ ch.reference.typeScope = allTypes ∧
         ch.reference.period = rc.baseline ∧ ch.compared.period = p) ∧
  (∀ K ∈ L.criterion; s : ScoreComponent; rc ∈ L.comparison •
     scoreDecrease(s) ∈ K.components ∧ conditionHolds(ctx, L.treatment, s.condition) ∧ rc.treatment = L.treatment ∧
     (∃ a ∈ ctx.subject.instrumentAdministrations • a.instrument = s.instrument ∧ rc.treatmentStart < a.date ∧
        inPeriod(a.date, last(L.evaluated))) ⇒
       ∃ r ∈ L.otherValues ∩ InstrumentResult • r.instrument = s.instrument ∧ evaluationResult(L, r) ∧
         ((∃ a ∈ ctx.subject.instrumentAdministrations • a.instrument = s.instrument ∧ a.date ≤ rc.treatmentStart) ⇒
            ∃ b ∈ r.baselineResult • pretreatmentBaseline(L, b))) ∧
  (∀ x : ControlLevel • L.category = controlLevel(x) ⇒ ∀ p ∈ ran L.evaluated • levelDays(L, p) ≠ ∅)
```
- Reading: A responder label has the criterion it applies, with its thresholds. It has a response comparison among whose on-treatment periods are the periods the label refers to, and the residual burden of every percentage change in migraine or headache days that this comparison shows for those periods. For each kind of value on which the criterion also rests that is available (`valueAvailable`, E-045), the label has values of that kind: for an instrument, a result of it and, where a result completed after the treatment start within the last period the label refers to is available, the result at the evaluation (`evaluationResult`, E-046); for the effectiveness of acute treatment, an acute-treatment summary of each acute medication the subject has used (`summarisesMedication`, E-051), over all headache types combined, for each evaluated period; for a kind of per-period value, values of that kind over all headache types combined, or, where the criterion names the values of one headache type, values in the scope `scopeFor` (E-012) of that type, for the baseline period of the response comparison and for each evaluated period, with, for acute-treatment summaries, a summary of each acute medication the subject has used; and, for another kind it names, a value of that kind. For each reduction component whose condition the label's treatment meets, the response comparison shows, for each of its measures that the diary provides, the change over all headache types combined from the baseline for each evaluated period. For each instrument-score component whose condition the label's treatment meets, where a result of the instrument completed after the treatment start within the last period the label refers to is available, the label has the result at the evaluation, with a baseline result (`pretreatmentBaseline`, E-046) where a result completed on or before the treatment start is available. The view of a control-level label shows the days with migraine or moderate-to-severe headache of each evaluated month (`levelDays`, E-046).
- Conformance: SHOULD. Scope: output.
- Realises: OUT-019, OUT-020
- Evidence: Stage 1 OUT-020, OUT-026, OUT-023, OUT-029; [S-010] INV-062/Q00.
- Notes: R-MCF (1), (4). Rationale: INV-062/D01, INV-062/D02, INV-062/D03, INV-062/S01, INV-062/S02.

### INV-114 A responder label's response comparison is one of the label's treatment
- Predicate:
```omn
∀ L : ResponderLabel; rc ∈ L.comparison • rc.treatment = L.treatment
```
- Reading: A response comparison that a responder label shows as its underlying values is the response comparison of the label's own treatment.
- Conformance: definitional (E-046). Scope: output.
- Realises: OUT-020
- Evidence: Stage 1 OUT-020 ("If the output displays a responder or non-responder label, it SHOULD name the criterion applied [...] and SHOULD always show the underlying values (OUT-018, OUT-019)"); OUT-018 ("For each preventive treatment, the diary output MUST compare monthly migraine days and monthly headache days").
- Notes: Rationale: INV-114/D01, INV-114/S01.

### INV-116 A criterion shown under the name of a named criterion is that criterion
- Predicate:
```omn
∀ L : ResponderLabel; K ∈ L.criterion; n ∈ namedCriteria • K.name = n.name ⇒
  K.alsoRestsOn = n.alsoRestsOn ∧ K.components ⊆ n.components ∧
  ∀ k ∈ n.components \ K.components •
    (∃ r : ReductionComponent • k = reductionFromBaseline(r) ∧ ¬ conditionHolds(ctx, L.treatment, r.condition)) ∨
    (∃ a : AttackReductionComponent • k = attackReduction(a) ∧ ¬ conditionHolds(ctx, L.treatment, a.condition)) ∨
    (∃ s : ScoreComponent • k = scoreDecrease(s) ∧ ¬ conditionHolds(ctx, L.treatment, s.condition))
```
- Reading: A criterion that a responder label shows under the name of one of the named criteria of E-045 (for example "NICE CG150 rec. 1.3.28") is that criterion: each of its components, with its threshold and condition, is a component of the named criterion; it leaves out only components whose condition the label's treatment does not meet (for example the threshold in chronic migraine of NICE 1.3.28 on the label of a treatment given for episodic migraine); and it rests on the same other values. So every threshold it shows is that of its source, and it shows every threshold of its source that applies to the label's treatment.
- Conformance: definitional (E-045, E-046). Scope: output.
- Realises: OUT-020
- Evidence: Stage 1 OUT-020, OUT-018; [S-015] INV-116/Q00.
- Notes: Rationale: INV-116/D01, INV-116/D02, INV-116/S01.

### INV-063 A responder label agrees with the decidable components of its criterion
- Predicate:
```omn
∀ L : ResponderLabel; K ∈ L.criterion •
  (controlLevels ∈ K.components ⇔ L.category is controlLevel) ∧
  ((L.category = responder ∨ L.category = nonResponder) ∧ evaluatedOnTreatment(L) ⇒
     ((∃ k ∈ K.components • componentMet(L, k)) ⇒ L.category = responder) ∧
     ((∀ k ∈ K.components • componentDecided(L, k) ∧ ¬ componentMet(L, k)) ⇒ L.category = nonResponder))
```
- Reading: A label is a control-level label exactly when its criterion has the control-levels component; INV-064 states the levels. For a responder or non-responder label: if any component of the named criterion is met by the values shown, the label is "responder". A reduction component is met by a reduction from baseline of at least the threshold in one of its measures, over all headache types combined, in the single on-treatment period the label refers to, in the response comparison of the label's treatment, from a baseline value above 0. An attack-reduction component is met by a reduction of at least the threshold from the number of attacks that the label shows for the baseline period of its response comparison, where that number is above 0, to the number it shows for that single on-treatment period, both of the headache types whose attacks the component counts: all types combined, or the subject's headaches of the type it names (over all types combined where the subject has a headache type and every headache type it has or may have falls under that type, and otherwise in the scope of that type). Values of another type scope, for example those of a single headache type of a subject who also has another type, neither meet nor decide a component; the reader applies the named criterion to them. An instrument-score component is met by a decrease of at least the threshold from the pre-treatment baseline score, in the stated range, to the score at the evaluation: from the latest result of the instrument completed on or before the treatment start to the latest result completed after it within the last period the label refers to. Each component counts only where the label's treatment meets its condition: a treatment given for episodic migraine, or for chronic migraine, or one to which the IHS Q6 situation applies (E-045, `conditionHolds`). If every component can be decided from the values shown and none is met, the label is "non-responder". A criterion with a judgement component is not decided by the values alone, so the model then requires only the relation for "responder". A reduction or attack-reduction component is decided only for a label that refers to one on-treatment period, because the cited criteria do not state how several periods are combined, and only where the baseline values it is tested on are above 0; a label over several periods is not decided by these components. A score component is decided only by the pair of results it compares; results that are both from before the treatment start, a baseline result that is not the latest one before the start, or a result outside the last evaluated period decide nothing. A label that refers to a period ending after a stop or pause of its treatment, the last day of the course (`evaluatedOnTreatment`, E-046), is decided by no component: the named criteria judge the response over the time on treatment, so the values of such a period neither force nor exclude a category, and the reader applies the named criterion to the values shown.
- Conformance: definitional (E-046). Scope: output.
- Realises: OUT-020
- Evidence: Stage 1 OUT-020, OUT-018; [S-008], [S-015], [S-033] INV-063/Q00.

### INV-064 Control levels of the IHS position statement 2025
- Predicate:
```omn
∀ L : ResponderLabel; x : ControlLevel • L.category = controlLevel(x) ⇒
  (∀ p ∈ ran L.evaluated • p.kind ∈ MonthlyKind) ∧ consecutive(L.evaluated) ∧
  (∀ p ∈ ran L.evaluated • courseBegunBy(ctx, L.treatment, p.start)) ∧ evaluatedOnTreatment(L) ∧
  (∀ p ∈ ran L.evaluated; n ∈ levelDays(L, p) • inControlRange(x, n)) ∧
  (∀ mm ∈ controlMinMonths(x) • #L.evaluated ≥ mm) ∧
  (∀ y : ControlLevel; t ∈ forcedAbove(y) • (∀ p ∈ ran L.evaluated • ∃ n ∈ levelDays(L, p) • n > t) ⇒ x = y)
```
- Reading: A control-level label refers to consecutive monthly periods, each beginning on or after a dated course event of the label's treatment (`courseBegunBy`, E-008; R-MCF (2)) and ending on or before the date of every stop or pause of it (`evaluatedOnTreatment`, E-046). The days with migraine or moderate-to-severe headache of every evaluated month lie in the range of the label's level (`inControlRange`, table SD-CL); a level with a least number of months (`controlMinMonths`, table SD-CL) refers to at least that many months; and where every evaluated month shows more days than the bound that table SD-CL gives for a level (`forcedAbove`), the label shows that level.
- Conformance: definitional (E-046). Scope: output.
- Realises: OUT-020
- Evidence: Stage 1 OUT-020; [S-010] INV-064/Q00.
- Notes: R-MCF (2). Rationale: INV-064/D01, INV-064/S01.

### INV-066 Adherence next to the response comparison
- Predicate:
```omn
∀ rc : ResponseComparison • ∃ a ∈ viewOf(rc).content ∩ AdherenceSummary • adherenceFor(a, rc)
```
- Reading: Each response comparison is shown with the patient-reported adherence to the treatment over an evaluation window that begins on or after the treatment start and contains one of its on-treatment periods, ending with it (`adherenceFor`, E-047).
- Conformance: SHOULD. Scope: output.
- Realises: OUT-039
- Evidence: Stage 1 OUT-039 ("over the evaluation window, next to the response comparison of OUT-018, so that a reader can see whether an apparent lack of effect coincided with inconsistent intake").
- Notes: Rationale: INV-066/D01, INV-066/S01.

### INV-067 Adherence refers to the time on treatment
- Predicate:
```omn
∀ a : AdherenceSummary • courseBegunBy(ctx, a.treatment, a.window.start)
```
- Reading: The window of an adherence summary begins on or after a dated course event of its treatment (`courseBegunBy`, E-008; R-MCF (2)).
- Conformance: definitional (E-047). Scope: output.
- Realises: OUT-039
- Evidence: Stage 1 OUT-039.
- Notes: R-MCF (2). Rationale: INV-067/D01.

### INV-068 Treatment review view: frequency and medication for the same periods
- Predicate:
```omn
∀ v : TreatmentReviewView • (∃ s ∈ startOf(ctx, v.treatment) • v.baseline.end < s ∧ ∀ p ∈ ran v.onTreatment • s ≤ p.start) ∧
  (∀ p ∈ ran v.onTreatment • notStoppedBefore(ctx, v.treatment, p.end)) ∧
  ∀ p ∈ {v.baseline} ∪ ran v.onTreatment • shownDay(v, headacheDays, p, allTypes) ∧
    (hasType(ctx, c1) ⇒ shownDay(v, migraineDays, p, allTypes)) ∧ shownDay(v, acuteMedicationDays(allAcuteMedication), p, allTypes) ∧
    ∀ m ∈ ctx.subject.acuteMedications • shownDay(v, acuteMedicationDays(ofClass(classOf(m.drug))), p, allTypes) ∧
      shownDay(v, acuteMedicationDays(ofDrug(m.drug)), p, allTypes)
```
- Reading: The treatment review view shows, for the same baseline and on-treatment periods (a baseline period that ends before a start of the treatment that the context states, and on-treatment periods that begin on or after it and end on or before the date of every stop or pause of the treatment, the last day of its course, section 2.8), headache days, migraine days (for patients with migraine) and acute-medication days, over all headache types combined: in total across classes, for each ICHD-3 8.2 class of the subject's acute medications, and for each of their drugs.
- Conformance: MUST. Scope: output.
- Realises: OUT-021
- Evidence: Stage 1 OUT-021 (MUST for OUT-004, OUT-005 and OUT-014 together; OUT-005 keeps its condition by the reference rule of section 3.5); the acute-medication days of OUT-014 ("broken down by drug class [...] and by individual drug, together with the total across classes"), as in INV-118 (C1-10, C1-13) and INV-104.
- Notes: R-MCF (1). Rationale: INV-068/D01, INV-068/S01, INV-068/W01.

### INV-069 Treatment review view: further dimensions where provided
- Predicate:
```omn
∀ v : TreatmentReviewView •
  (∀ p ∈ {v.baseline} ∪ ran v.onTreatment •
     (provides(ModerateSevereHeadacheDays) ⇒ shownDay(v, moderateSevereHeadacheDays, p, allTypes)) ∧
     (provides(AttackCount) ⇒ ∃ m ∈ v.content ∩ AttackCount • m.period = p ∧ m.typeScope = allTypes) ∧
     (hasType(ctx, c1) ∧ provides(MostBothersomeSymptomItem) ⇒
        ∃ m ∈ v.content ∩ MostBothersomeSymptomItem • m.period = p ∧ m.typeScope = allTypes) ∧
     (provides(AcuteTreatmentSummary) ⇒ ∀ am ∈ ctx.subject.acuteMedications •
        ∃ s ∈ v.content ∩ AcuteTreatmentSummary • summarisesMedication(s, am) ∧ s.period = p ∧ s.typeScope = allTypes)) ∧
  (provides(IntensitySummary) ⇒ ∃ i₁ ∈ v.content ∩ IntensitySummary • ∀ p ∈ {v.baseline} ∪ ran v.onTreatment •
     ∃ m ∈ v.content ∩ IntensitySummary • m.period = p ∧ m.typeScope = allTypes ∧ onSameScale(m, i₁)) ∧
  (hasType(ctx, c1) ∧ provides(AssociatedSymptomSummary) ⇒ ∀ s : AssociatedSymptom • ∃ a₁ ∈ v.content ∩ AssociatedSymptomSummary •
     ∀ p ∈ {v.baseline} ∪ ran v.onTreatment •
       ∃ m ∈ v.content ∩ AssociatedSymptomSummary • m.period = p ∧ m.typeScope = allTypes ∧ m.symptom = s ∧ inSameForm(m, a₁)) ∧
  (provides(InstrumentResult) ⇒ ∀ i : Instrument •
     let A == {a ∈ ctx.subject.instrumentAdministrations | a.instrument = i ∧ a.date ≤ last(v.onTreatment).end • a.date} •
       A ≠ ∅ ⇒ ∃ r ∈ v.content ∩ InstrumentResult • r.instrument = i ∧ r.completionDate = {max A})
```
- Reading: Where the diary provides them, the treatment review view also shows, for the same periods and over all headache types combined, moderate/severe headache days, attacks, intensity (the summaries of all these periods on one scale and in one form, `onSameScale`, E-023), migraine-associated symptoms (the summaries of each symptom in one form for all these periods, `inSameForm`, E-025) and the most bothersome symptom (both for migraine), and the effectiveness of each acute medication for the attacks treated in each period (an acute-treatment summary of all formulations of its drug or of its own formulation, `summarisesMedication`, E-051, whose outcome summaries and treated-attack lines E-051 `outcomes` and `sequence` (W2) place in the same view), together with the most recent result of each instrument (including PGIC and any other validated instrument whose results are available, E-057) up to the end of the last on-treatment period.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-021, OUT-023
- Evidence: Stage 1 OUT-021, OUT-023 ("so that a change in the response to acute treatment after the start of prevention is visible (see OUT-021)").
- Notes: R-MCF (4). Rationale: INV-069/D01, INV-069/S01.

### INV-070 Post-stop monitoring content
- Predicate:
```omn
∀ v : PostStopMonitoringView •
  ∀ p ∈ v.baseline ∪ v.onTreatmentPeriod ∪ ran v.after • shownDay(v, headacheDays, p, allTypes) ∧ shownDay(v, migraineDays, p, allTypes)
```
- Reading: After a stop, pause or dose reduction of a preventive treatment, the view shows headache days and migraine days for each of its periods after the event, for its on-treatment period and for its original pre-treatment baseline period, so that worsening or rebound above baseline is visible.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-022
- Evidence: Stage 1 OUT-022; [S-011], [S-022] INV-070/Q00.
- Notes: R-MCF (2). Rationale: INV-070/S01.

### INV-112 Post-stop monitoring periods are those of the event
- Predicate:
```omn
∀ v : PostStopMonitoringView • (∀ b ∈ v.baseline • ∃ s ∈ originalStart(ctx, v.treatment) • b.end < s) ∧ consecutive(v.after) ∧
  (∀ x ∈ firstChangedDay(v.event, v.eventDate) •
     (∀ q ∈ v.onTreatmentPeriod • courseBegunBy(ctx, v.treatment, q.start) ∧ q.end < x) ∧
     (v.after ≠ ∅ ⇒ first(v.after).start = x))
```
- Reading: The periods of a post-stop monitoring view: its periods after the event are consecutive and begin on the first day of the changed regimen (`firstChangedDay`, E-049: the first day off treatment, the day after the stop or pause date, which is the last day of the course; or the first day at the reduced dose, the date of the reduction); its on-treatment period begins on or after a dated course event of the course (`courseBegunBy`, E-008; R-MCF (2)) and ends before that day; and a baseline period it shows ends before a start that the context states for the treatment as it was first started (`originalStart`, E-008; R-MCF (1)).
- Conformance: definitional (E-049). Scope: output.
- Realises: OUT-022
- Evidence: Stage 1 OUT-022; [S-011], [S-022] INV-112/Q00.
- Notes: R-MCF (1), (2). Rationale: INV-112/D01, INV-112/D02, INV-112/S01.

### 6.7 Acute treatment

### INV-071 Acute-treatment summaries per drug, per formulation and per preventive phase
- Predicate:
```omn
∀ c ∈ Ctx; m ∈ c.subject.acuteMedications •
  (∃ o : Output • (c, o) ∈ Rep ∧
     (∃ s ∈ parts(o) ∩ AcuteTreatmentSummary • s.drug = m.drug ∧ s.formulationScope = allFormulations ∧ s.typeScope = allTypes ∧
        sameSpan(s.period, c.timeRange)) ∧
     (∃ s ∈ parts(o) ∩ AcuteTreatmentSummary • s.drug = m.drug ∧ s.formulationScope = singleFormulation ∧
        s.formulations = {m.formulation} ∧ s.typeScope = allTypes ∧ sameSpan(s.period, c.timeRange))) ∧
  (∀ t ∈ c.subject.preventiveTreatments • startOf(c, t) ≠ ∅ ⇒
     ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views; rc ∈ v.content ∩ ResponseComparison • rc.treatment = t ∧
       ∀ p ∈ {rc.baseline} ∪ ran rc.onTreatment • ∃ s ∈ v.content ∩ AcuteTreatmentSummary • summarisesMedication(s, m) ∧ s.period = p ∧
         s.typeScope = allTypes)
```
- Reading: For each acute medication the subject has used up to the as-of date (E-008), including one it no longer uses, its effectiveness across the attacks treated with it, over all headache types combined, is available for the selected time range, for all its formulations and separately for each formulation; and for each preventive treatment whose start the context states, it is available separately for the pre-treatment baseline period and each on-treatment period, next to the response comparison, as a summary of all formulations of its drug or of its own formulation (`summarisesMedication`, E-051), with the outcome summaries and attack lines of each summary in the same view (E-051 `outcomes`, `sequence` (W2)).
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-021, OUT-023
- Evidence: Stage 1 OUT-023.
- Notes: R-MCF (1).

### INV-072 Acute-treatment summary content
- Predicate:
```omn
∀ s : AcuteTreatmentSummary • (∀ k ∈ requiredOutcomes(s.earlyTimePoint) • ∃ os ∈ s.outcomes • os.measure = k) ∧
  #s.sequence = s.treatedAttacks ∧
  (∀ l ∈ ran s.sequence • l.intakeTiming ≠ ∅ ∧
     ∀ k ∈ requiredOutcomes(s.earlyTimePoint) • ∃ b : 𝔹 • AttackOutcomeResult(measure ↦ k, achieved ↦ b) ∈ l.results) ∧
  (s.formulationScope = allFormulations ⇒
     ∀ am ∈ ctx.subject.acuteMedications • am.drug = s.drug ⇒ am.formulation ∈ s.formulations)
```
- Reading: An acute-treatment summary has an outcome summary for every outcome measure of its time point (pain freedom, absence of the most bothersome symptom, headache relief and non-pain-symptom status at 2 hours or 15 minutes; sustained pain freedom, maintained relief and maintained non-pain-symptom status to 24 hours; rescue or repeat medication; relapse; drug-related adverse events and whether they were regarded as meaningful). It lists every treated attack it summarises, in order, and each attack line shows the result of every one of these outcome measures and when the medication was taken relative to onset or the pain intensity at intake. A summary of all formulations of a drug states every formulation or route of the subject's acute medications of that drug, that is, every one that the subject has used up to the as-of date.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-012, OUT-021, OUT-023, OUT-031
- Evidence: Stage 1 OUT-012 ("both across periods and in the response of individual treated attacks (see OUT-023)"), OUT-021 ("the same view SHOULD also include [...] the effectiveness of acute treatment for the attacks treated in each of these periods (OUT-023)"), OUT-023 ("For each acute medication, the diary output SHOULD report, across the attacks treated with it, the outcome measures [...]"; "SHOULD show how consistently the drug was effective across consecutive treated attacks"; "The output SHOULD also state the formulation or route of administration (for example oral or subcutaneous) of each acute medication it summarises"), OUT-031.
- Notes: A summary may have 0 treated attacks; it then shows its outcome summaries with 0 attacks assessed and no lines (INV-074). Rationale: INV-072/D01, INV-072/D02.

### INV-073 Early time point: 15 minutes for cluster headache, otherwise 2 hours
- Predicate:
```omn
∀ s : AcuteTreatmentSummary •
  (∀ tp : EarlyTimePoint; t ∈ earlyTimePointType(tp) • onlyOfType(ctx, s.typeScope, t) ⇒ s.earlyTimePoint = tp) ∧
  ((¬ ∃ tp : EarlyTimePoint; t ∈ earlyTimePointType(tp) • onlyOfType(ctx, s.typeScope, t)) ⇒ s.earlyTimePoint = twoHours)
```
- Reading: Summaries of treated attacks of cluster headache only use the 15-minute time point (`earlyTimePointType`, table SD-ET); all others use 2 hours. A summary over all headache types is one of cluster headache only when the subject has cluster headache and every headache type it has, or may have, is cluster headache.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-023, OUT-031
- Evidence: Stage 1 OUT-023 ("For cluster headache, the corresponding time point is 15 minutes"), OUT-031; OUT-029 ("When the patient has, or may have, more than one headache type") for the type scope.
- Notes: Rationale: INV-073/D01.

### INV-074 Outcome counts agree with the summary and its attack lines
- Predicate:
```omn
(∀ os : OutcomeSummary • os ∈ os.summary.outcomes ∧ os.attacksWithOutcome ≤ os.attacksAssessed ∧ os.attacksAssessed ≤ os.summary.treatedAttacks ∧
   (∀ q ∈ os.proportion • os.attacksAssessed > 0 ∧ q ≈ 100 × os.attacksWithOutcome ÷ os.attacksAssessed) ∧
   (∀ tp : EarlyTimePoint • os.measure ∈ {painFreedom(tp), mostBothersomeSymptomAbsent(tp), headacheRelief(tp), nonPainSymptomsAbsentOrMinimal(tp)} ⇒
      tp = os.summary.earlyTimePoint) ∧
   (#os.summary.sequence = os.summary.treatedAttacks ⇒
      os.attacksAssessed = #{l ∈ ran os.summary.sequence | ∃ b : 𝔹 • AttackOutcomeResult(measure ↦ os.measure, achieved ↦ b) ∈ l.results} ∧
      os.attacksWithOutcome = #{l ∈ ran os.summary.sequence | AttackOutcomeResult(measure ↦ os.measure, achieved ↦ true) ∈ l.results})) ∧
(∀ s : AcuteTreatmentSummary • (∀ os ∈ s.outcomes • os.summary = s) ∧ (∀ o₁, o₂ ∈ s.outcomes • o₁.measure = o₂.measure ⇒ o₁ = o₂) ∧
   #s.sequence ≤ s.treatedAttacks ∧ (∀ i ∈ dom s.sequence • i < #s.sequence ⇒ s.sequence(i).onset ≤ s.sequence(i + 1).onset) ∧
   (∀ i, j ∈ dom s.sequence • s.sequence(i) = s.sequence(j) ⇒ i = j) ∧
   (∀ l ∈ ran s.sequence • l.drug = s.drug ∧ inPeriod(l.onset, s.period) ∧
      (s.formulationScope = singleFormulation ∨ s.formulations ≠ ∅ ⇒ ∀ f ∈ l.formulation • f ∈ s.formulations)) ∧
   (s.formulationScope = singleFormulation ⇒ #s.formulations ≤ 1))
```
- Reading: For each outcome, the attacks with the outcome do not exceed the attacks for which it is shown, which do not exceed the attacks the summary covers; a proportion is shown only where the outcome is shown for at least one attack, and is the one divided by the other; the time point of the outcome is the summary's; when the summary lists all its attacks, its counts are those of its lines. An outcome summary is one of the outcomes of its summary, which has one outcome summary per measure. A summary lists at most the attacks it covers, in order, once each, all of its drug and period and, where a line shows its formulation, of a formulation that the summary names: always for a single formulation, and for all formulations wherever the summary names its formulations; a summary of a single formulation names at most one formulation.
- Conformance: definitional (E-051, E-052). Scope: output.
- Realises: OUT-023
- Evidence: Stage 1 OUT-023 ("The output SHOULD also state the formulation or route of administration (for example oral or subcutaneous) of each acute medication it summarises").
- Notes: Rationale: INV-074/D01.

### INV-075 Attack lines are consistent
- Predicate:
```omn
∀ l : TreatedAttackLine • (∀ r₁, r₂ ∈ l.results • r₁.measure = r₂.measure ⇒ r₁ = r₂) ∧
  (∀ s₁, s₂ ∈ l.symptomStatus • s₁.symptom = s₂.symptom ⇒ s₁ = s₂) ∧
  (AttackOutcomeResult(measure ↦ drugRelatedAdverseEvent, achieved ↦ false) ∈ l.results ⇒ l.adverseEvents = ∅) ∧
  (AttackOutcomeResult(measure ↦ adverseEventRegardedMeaningful, achieved ↦ true) ∈ l.results ⇒
     AttackOutcomeResult(measure ↦ drugRelatedAdverseEvent, achieved ↦ true) ∈ l.results) ∧
  (∀ ae ∈ l.adverseEvents • true ∈ ae.regardedMeaningful ⇒
     AttackOutcomeResult(measure ↦ adverseEventRegardedMeaningful, achieved ↦ false) ∉ l.results)
```
- Reading: A treated-attack line shows each outcome once and the status of each associated symptom once; it lists adverse events only when it shows a drug-related adverse event; a meaningful adverse event is a drug-related adverse event; and an adverse event the patient regarded as meaningful is not contradicted by the line's results.
- Conformance: definitional (E-053). Scope: output.
- Realises: OUT-012, OUT-023
- Evidence: Stage 1 OUT-012, OUT-023.
- Notes: Rationale: INV-075/D01.

### INV-076 Associated symptoms in the response of treated attacks, for migraine
- Predicate:
```omn
∀ l : TreatedAttackLine • hasType(ctx, c1) ⇒ ∀ a : AssociatedSymptom • ∃ st ∈ l.symptomStatus • st.symptom = a
```
- Reading: For a subject with migraine, each treated-attack line shows whether nausea/vomiting, photophobia and phonophobia were present at the early time point.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-012
- Evidence: Stage 1 OUT-012 ("both across periods and in the response of individual treated attacks (see OUT-023)").
- Notes: Rationale: INV-076/D01.

### 6.8 Treatment history and scheme windows

### INV-077 Treatment history lists every treatment
- Predicate:
```omn
∀ c ∈ Ctx • ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ TreatmentHistoryView •
  (∀ t ∈ c.subject.preventiveTreatments • ∃ g ∈ ran v.preventiveGroups; l ∈ ran g.lines • l.treatment = t) ∧
  (∀ t ∈ c.subject.acuteTreatments • ∃ g ∈ ran v.acuteGroups; l ∈ ran g.lines • l.treatment = t)
```
- Reading: A treatment history is available that lists every preventive treatment and, separately, every acute treatment of the subject.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-024
- Evidence: Stage 1 OUT-024.

### INV-078 Treatment history is chronological and grouped by drug class
- Predicate:
```omn
∀ v : TreatmentHistoryView • (∀ g ∈ ran v.preventiveGroups • g.role = preventive) ∧ (∀ g ∈ ran v.acuteGroups • g.role = acute) ∧
  (∀ g₁, g₂ ∈ ran v.preventiveGroups • g₁.drugClass = g₂.drugClass ⇒ g₁ = g₂) ∧
  (∀ g₁, g₂ ∈ ran v.acuteGroups • g₁.drugClass = g₂.drugClass ⇒ g₁ = g₂) ∧
  ∀ g ∈ ran v.preventiveGroups ∪ ran v.acuteGroups •
    (∀ l ∈ ran g.lines • l ∈ v.content ∧ l.role = g.role ∧ drugClassOf(l.drug) = g.drugClass) ∧
    (∀ i, j ∈ dom g.lines • i < j ⇒ ∀ a ∈ g.lines(i).startDate; b ∈ g.lines(j).startDate • a ≤ b) ∧
    (∀ l ∈ ran g.lines; g₂ ∈ ran v.preventiveGroups ∪ ran v.acuteGroups • l ∈ ran g₂.lines ⇒ g₂ = g)
```
- Reading: Preventive and acute treatments are listed separately; within each, treatments are grouped by drug class (one group per class), the treatment lines of every group are shown in the view, each treatment appears in one group, and within a group treatments are in order of their start dates: every two lines that show a start date are in the order of these dates, also where a line without a start date lies between them.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-024
- Evidence: Stage 1 OUT-024 ("a chronological list [...] grouped by drug class").
- Notes: R-MCF (1). Rationale: INV-078/D01, INV-078/D02.

### INV-079 Treatment lines agree with the treatment course
- Predicate:
```omn
∀ l : TreatmentLine • l.drug = drugOf(l.treatment) ∧
  (∀ s ∈ l.startDate; e ∈ l.stopDate • s ≤ e ∧ ∀ d ∈ l.duration • d = daysLong(days(s, e))) ∧
  (¬ stopped(ctx, l.treatment) ⇒ ∀ s ∈ l.startDate; d ∈ l.duration • s ≤ ctx.asOf ∧ d = daysLong(days(s, ctx.asOf))) ∧
  (∀ d ∈ l.duration • startOf(ctx, l.treatment) ≠ ∅) ∧
  (∀ d ∈ l.duration; s ∈ startOf(ctx, l.treatment) •
     (∀ e ∈ ctx.subject.courseEvents • e.treatment = l.treatment ∧ e.kind is stop ⇒ s ≤ e.date ∧ d = daysLong(days(s, e.date))) ∧
     (¬ stopped(ctx, l.treatment) ⇒ s ≤ ctx.asOf ∧ d = daysLong(days(s, ctx.asOf)))) ∧
  (∀ r ∈ l.preventiveResponse • r.treatment = l.treatment) ∧ (∀ a ∈ l.adherence • a.treatment = l.treatment) ∧
  (∀ s ∈ l.acuteResponse • s.drug = l.drug)
```
- Reading: A treatment line shows the drug of its treatment; a stop date not before the start date; a duration equal to the days from the start of the course to its stop or, for a treatment that has not stopped, from its start to the as-of date of the output (its duration to date), whether or not the line shows its start and stop dates, and no duration for a treatment whose start the context does not state; and the response summary and adherence of the same treatment.
- Conformance: definitional (E-055). Scope: output.
- Realises: OUT-024, OUT-039
- Evidence: Stage 1 OUT-024; [S-013] INV-079/Q00.
- Notes: R-MCF (1). Rationale: INV-079/D01, INV-079/W01.

### INV-109 A treatment line shows every dose change, and its response summary and adherence with it
- Predicate:
```omn
∀ l : TreatmentLine •
  (∀ e ∈ ctx.subject.courseEvents; k : DoseChangeDirection • e.treatment = l.treatment ∧ e.kind = doseChange(k) ⇒
     ∃ dc ∈ l.doseChanges • dc.date = e.date ∧ dc.direction = k) ∧
  (l.role = acute ⇒ ∀ m ∈ ctx.subject.acuteMedications • m.drug = l.drug ⇒
     ∃ s ∈ l.acuteResponse • s.typeScope = allTypes ∧ summarisesMedication(s, m) ∧
     (∀ b ∈ startOf(ctx, l.treatment) • s.period.start = b) ∧
     (∀ f ∈ ctx.subject.courseEvents • f.treatment = l.treatment ⇒ s.period.start ≤ f.date) ∧
     (stopped(ctx, l.treatment) ⇒ (∃ k : StopKind • eventOn(ctx, l.treatment, stop(k), s.period.end)) ∧
        ∀ e ∈ l.stopDate • s.period.end = e) ∧
     (¬ stopped(ctx, l.treatment) ⇒ s.period.end = ctx.asOf)) ∧
  (∀ a ∈ l.adherence • ∀ r ∈ l.preventiveResponse • adherenceFor(a, r))
```
- Reading: A treatment line shows every dose change of its treatment, with its date and direction. An acute treatment line has, for each acute medication of the treatment's drug that the subject has used, an acute-treatment summary over all headache types combined, of all formulations of the drug or of that medication's formulation (`summarisesMedication`, E-051), that covers the span of its course: from its start (where the context states no start, from on or before its first dated course event) to its stop (on the stop date that the line shows, where it shows one) or, for a treatment that has not stopped, to the as-of date. The adherence of a line is over an evaluation window of the response comparison it shows (`adherenceFor`, E-047).
- Conformance: SHOULD. Scope: output.
- Realises: OUT-024, OUT-034, OUT-039
- Evidence: Stage 1 OUT-024 ("a chronological list of preventive (and, separately, acute) treatments with start and stop dates, dose changes, treatment duration, the response summary from OUT-018 or OUT-023 for each treatment, adverse effects during each treatment, and the reason for stopping"), OUT-034 ("current and past treatments with response (OUT-018, OUT-023, OUT-024)"), OUT-039 ("The adherence output SHOULD also be available in the treatment history (OUT-024) and in the clinician-facing summary (OUT-034)").
- Notes: R-MCF (2). Rationale: INV-109/D01, INV-109/D02, INV-109/D03, INV-109/D04, INV-109/D05, INV-109/S01.

### INV-080 Scheme windows are the selected windows
- Predicate:
```omn
∀ v : SchemeWindowView • ∃ sel ∈ ctx.schemeSelection • v.scheme = sel.scheme ∧ #v.windows = #sel.windows ∧
  ∀ i ∈ dom v.windows • sameSpan(v.windows(i), sel.windows(i))
```
- Reading: A scheme-window view shows exactly the windows the clinician selected and is labelled with the selected scheme.
- Conformance: definitional (E-056). Scope: output.
- Realises: OUT-025
- Evidence: Stage 1 OUT-025.
- Notes: R-MCF (3).

### 6.9 Instruments

### INV-081 Results of validated instruments where available
- Predicate:
```omn
∀ c ∈ Ctx; a ∈ c.subject.instrumentAdministrations • inSpan(a.date, c.timeRange) ⇒
  ∃ o : Output • (c, o) ∈ Rep ∧ ∃ r ∈ parts(o) ∩ InstrumentResult • r.instrument = a.instrument ∧ r.completionDate = {a.date} ∧
    ((∃ b ∈ c.subject.instrumentAdministrations • b.instrument = a.instrument ∧ b.date < a.date) ⇒ r.baselineResult ≠ ∅)
```
- Reading: Every available instrument result in the selected time range is reported, and, where an earlier administration of the same instrument exists, it is shown with its baseline administration.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-026
- Evidence: Stage 1 OUT-026.
- Notes: R-MCF (4).

### INV-082 Instrument results agree with the instrument's published value set
- Predicate:
```omn
∀ r : InstrumentResult •
  (r.instrument ∈ dom scoreRange ⇒ ∀ x ∈ r.totalScore • x ≥ scoreRange(r.instrument).low ∧ ∀ h ∈ scoreRange(r.instrument).high • x ≤ h) ∧
  (r.instrument ∈ wholeNumberScores ⇒ ∀ x ∈ r.totalScore • x ∈ ℕ) ∧
  (∀ cat ∈ r.category • banded(r.instrument) ⇒ ∃ b ∈ gradeBands • cat = band(b) ∧ b.instrument = r.instrument ∧ ∀ x ∈ r.totalScore • inBand(x, b)) ∧
  (∀ cat ∈ r.category; b : GradeBand • cat = band(b) ⇒ b ∈ gradeBands ∧ b.instrument = r.instrument) ∧
  (∀ cat ∈ r.category • publishedGrading(r.instrument)) ∧
  (r.instrument ∈ dom publishedRecall ⇒ ∀ rp ∈ r.recallPeriod • rp = publishedRecall(r.instrument)) ∧
  (∀ b ∈ r.baselineResult • b.instrument = r.instrument ∧ b ≠ r ∧ ∀ d₁ ∈ b.completionDate; d₂ ∈ r.completionDate • d₁ < d₂) ∧
  (∀ ch ∈ r.changeFromBaseline; b ∈ r.baselineResult; x ∈ r.totalScore; y ∈ b.totalScore • ch = x − y)
```
- Reading: A total score lies in the instrument's score range (table SD-IN: 36–78 for HIT-6; at least 0 for MIDAS, PedMIDAS and HALT, for which the model states no upper bound) and is a whole number for HIT-6, MIDAS, PedMIDAS, HALT-90 and HALT-30; a grade or category is shown only for an instrument whose developer publishes a grading or categories, so never for HALT-30, which has no grading; the grade or category shown is, for MIDAS, HIT-6, PedMIDAS and HALT-90, a published band of that instrument that contains the score (table SD-GB), and, for every other instrument, a category as published, never a band of another instrument; the recall period shown is the instrument's published recall period (3 months for MIDAS, PedMIDAS and HALT-90, 1 month for HIT-6 and HALT-30); the baseline administration is an earlier result of the same instrument; the change from baseline is the score minus the baseline score.
- Conformance: definitional (E-057, E-058). Scope: output.
- Realises: OUT-026, OUT-036
- Evidence: Stage 1 OUT-026, OUT-036; [S-014], [S-101], [S-102], [S-103] INV-082/Q00.
- Notes: Rationale: INV-082/D01.

### INV-083 Screening results next to the headache outputs
- Predicate:
```omn
∀ c ∈ Ctx; a ∈ c.subject.screeningAdministrations • inSpan(a.date, c.timeRange) ⇒
  ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views; r ∈ v.content ∩ ScreeningResult •
    r.instrument = a.instrument ∧ r.date = {a.date} ∧ r.scores ≠ ∅ ∧
    (a.instrument = hads ⇒ ∀ sb ∈ {anxietySubscale, depressionSubscale} • ∃ s ∈ r.scores • s.subscale = sb) ∧
    ∃ m ∈ v.content ∩ HeadacheDays • m.typeScope = allTypes
```
- Reading: Every available depression or anxiety screening result in the selected time range is reported with instrument name, date and score (for HADS, both its anxiety and its depression subscale scores), in a view that also shows headache outputs.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-033
- Evidence: Stage 1 OUT-033; [S-104] INV-083/Q00.
- Notes: R-MCF (4). Rationale: INV-083/D01.

### INV-085 Screening scores lie in the instrument's range
- Predicate:
```omn
∀ r : ScreeningResult • (∀ s₁, s₂ ∈ r.scores • s₁.subscale = s₂.subscale ⇒ s₁ = s₂) ∧
  ((∃ sb : Subscale • (r.instrument, sb) ∈ dom screeningMax) ⇒
     ∀ s ∈ r.scores • (r.instrument, s.subscale) ∈ dom screeningMax ∧ s.score ≤ screeningMax(r.instrument, s.subscale))
```
- Reading: A screening result shows each subscale once; for an instrument whose score ranges table SD-SR states (HADS: anxiety and depression subscales, 0 to 21 each; PHQ-9 and GAD-7: the whole scale, 0 to 27 and 0 to 21), every score is of a subscale that the table names for it and does not exceed its highest score.
- Conformance: definitional (E-059). Scope: output.
- Realises: OUT-033
- Evidence: Stage 1 OUT-033; [S-104], [S-105] INV-085/Q00.
- Notes: Rationale: INV-085/D01.

### 6.10 Special populations and classification support

### INV-086 Menstrual-relation view for patients who menstruate
- Predicate:
```omn
∀ c ∈ Ctx • menstruatesDuring(c, c.timeRange) ⇒
  ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ MenstrualRelationView • sameSpan(v.covers, c.timeRange)
```
- Reading: For a selected time range during which the subject menstruates, at least in part, the diary can show migraine attacks and migraine days in relation to menstruation across consecutive cycles for that time range, with the perimenstrual window and the number of complete cycles.
- Conformance: MUST. Scope: repertoire.
- Realises: OUT-030
- Evidence: Stage 1 OUT-030.
- Notes: See ISS-03. Rationale: INV-086/D01.

### INV-087 Menstrual cycles, the perimenstrual window and attacks
- Predicate:
```omn
(∀ cl : CycleLine •
   (¬ cl.complete ⇒ cl.cycle.to = viewOf(cl).covers.end ∧ cl.nextWindowDays = ∅) ∧
   (cl.complete ⇒ cl.nextWindowDays =
      {DateSpan(from ↦ max {plusDays(cl.cycle.to, 1 − windowDaysBefore), cl.cycle.from}, to ↦ cl.cycle.to)}) ∧
   (cl.dayOneShown ⇒ cl.menstruationDays ≠ ∅ ∧ cl.cycle.from = min cl.menstruationDays ∧
      cl.firstDayOfMenstruation = {cl.cycle.from} ∧
      cl.perimenstrualWindow = {DateSpan(from ↦ plusDays(cl.cycle.from, − windowDaysBefore),
                                         to ↦ plusDays(cl.cycle.from, windowDaysAfter))}) ∧
   (¬ cl.dayOneShown ⇒ cl.cycle.from = viewOf(cl).covers.start ∧ cl.firstDayOfMenstruation = ∅ ∧ cl.perimenstrualWindow = ∅ ∧
      ∀ cl₂ : CycleLine • ∀ d ∈ cl₂.firstDayOfMenstruation • cl.cycle.to < d) ∧
   (∀ d ∈ cl.menstruationDays • inSpan(d, cl.cycle)) ∧ (∀ d ∈ cl.migraineDays • inSpan(d, cl.cycle)) ∧
   ∀ a ∈ cl.attacks • inSpan(a.onset, cl.cycle)) ∧
(∀ a : AttackMark • (∃₁ cl ∈ viewOf(a).content ∩ CycleLine • a ∈ cl.attacks) ∧
   (a.inPerimenstrualWindow ⇔ ∃ cl ∈ viewOf(a).content ∩ CycleLine • a ∈ cl.attacks ∧
      ((∃ w ∈ cl.perimenstrualWindow • inSpan(a.onset, w)) ∨ (∃ w ∈ cl.nextWindowDays • inSpan(a.onset, w))))) ∧
(∀ v : MenstrualRelationView • v.content ∩ CycleLine = ran v.cycles ∧
   v.completeCycles = #{cl ∈ ran v.cycles | cl.dayOneShown ∧ cl.complete ∧ v.covers.start ≤ cl.cycle.from ∧ cl.cycle.to ≤ v.covers.end} ∧
   (∀ i ∈ dom v.cycles • i < #v.cycles ⇒ v.cycles(i).complete ∧ v.cycles(i + 1).dayOneShown ∧
      v.cycles(i + 1).cycle.from = next(v.cycles(i).cycle.to)) ∧
   (∀ cl ∈ ran v.cycles • cl.cycle.from ≤ v.covers.end ∧ v.covers.start ≤ cl.cycle.to) ∧
   first(v.cycles).cycle.from ≤ v.covers.start ∧ v.covers.end ≤ last(v.cycles).cycle.to)
```
- Reading: Every cycle line, in whichever view it is shown, either begins on its first day of menstruation (day 1), which it shows, or is a lead-in: it begins on the first day of the period its view covers, shows no day 1 and no window of its own, and ends before every first day of menstruation that the output shows. A line shows its menstruation days and migraine days within the line, and, if it has not ended, is shown to the last day of the period its view covers. The perimenstrual window of a cycle runs from 2 days before to 2 days after day 1 (days −2 to +3, there being no day 0). A line that has ended (a cycle or a lead-in) shows its days that lie in the window of the next menstruation, whose day 1 is the day after its last day: its last two days, days −2 and −1 of that menstruation. The attacks of a line lie in the line. Every attack mark, in whichever view it is shown, is an attack of exactly one cycle line of that view, and it is marked as in the window exactly when its onset is a window day of a menstruation that this line shows: one of days +1 to +3 of its own menstruation, or, if the line has ended, one of days −2 and −1 of the next menstruation. The menstrual-relation view shows, as its own items and as its only cycle lines, the consecutive lines that overlap its period: the first is the cycle in progress on the first day of the period or a lead-in from that day, every later line shows its day 1, the last reaches the last day of the period, and every line except the last has ended. The number of complete cycles stated is the number of these lines that show their day 1, have ended and lie wholly within the period the view covers.
- Conformance: definitional (E-060, E-061). Scope: output.
- Realises: OUT-030, OUT-035
- Evidence: Stage 1 OUT-030, OUT-035; [S-001] INV-087/Q00.
- Notes: Relations: INV-124. The window of a menstruation begins two days before its day 1, in the previous line. A line that has ended therefore shows, as `nextWindowDays`, its days that are days −2 and −1 of the next menstruation: `plusDays(cl.cycle.to, 1 − windowDaysBefore)` is day −2 of the next menstruation and `cl.cycle.to` is day −1; the span is cut at the first day of the line, so that it contains only days of the line. Neither a lead-in, nor a cycle that began before the covered period, nor one that ends after it is counted in `completeCycles`. The relations of the derived attributes (`firstDayOfMenstruation`, `perimenstrualWindow`, `nextWindowDays`, `inPerimenstrualWindow`), the rules for lead-ins and the attachment of every attack mark to one cycle line hold in every view, including the patient-facing overview (INV-105); the structure of a sequence of lines and `completeCycles` belong to the menstrual-relation view. Rationale: INV-087/D01.

### INV-088 Cluster-headache view
- Predicate:
```omn
∀ c ∈ Ctx • hasType(c, c3_1) ⇒ ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ ClusterView • sameSpan(v.covers, c.timeRange) ∧
  (∀ b ∈ ran v.bouts; k : RateBasis • (∀ s ∈ b.start • s ≤ v.covers.end) ∧ (∀ e ∈ lastDay(b) • v.covers.start ≤ e) ⇒
     ∃ r ∈ v.rates • r.bout = b ∧ r.basis = k ∧ scopeFor(c, r.typeScope, c3_1)) ∧
  (∀ m ∈ c.subject.acuteMedications • ∃ s ∈ v.acute • summarisesMedication(s, m) ∧ s.period = v.covers ∧ scopeFor(c, s.typeScope, c3_1) ∧
     s.earlyTimePoint = fifteenMinutes ∧ ∃ os ∈ s.outcomes • os.measure = rescueOrRepeatMedication)
```
- Reading: For patients with cluster headache, a cluster-headache view of the selected time range is available. For every cluster period (bout) that it refers to and that overlaps the selected time range, it refers to attacks per day and per week; for each acute medication, it shows effectiveness at 15 minutes and the need for rescue treatment in the selected time range, the period the view covers, in a summary of all formulations of its drug or of its own formulation (`summarisesMedication`, E-051). The rates and the acute-treatment summaries it is required to show are those of all the subject's attacks of cluster headache: over all headache types combined where the subject has a headache type (here, cluster headache) and every headache type it has or may have is cluster headache or a subtype of it, and otherwise in the scope of cluster headache itself (`scopeFor`, E-012). It refers to its cluster periods, including previous bouts, and its remission periods as E-062 states.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-031
- Evidence: Stage 1 OUT-031; OUT-029 ("When the patient has, or may have, more than one headache type") for the type scope of the rates and summaries, as in INV-089.
- Notes: Rationale: INV-088/D01, INV-088/S01.

### INV-089 Cluster periods, remissions and rates are consistent
- Predicate:
```omn
(∀ x : ClusterPhaseItem • (x.ongoing ⇒ x.end = ∅) ∧ (∀ e ∈ x.end • e ≤ ctx.asOf) ∧
   (∀ s ∈ x.start; e ∈ lastDay(x) • s ≤ e ∧ ∀ d ∈ x.duration • d = daysLong(days(s, e))) ∧
   (x ∈ RemissionPeriodItem ⇒ ∀ s ∈ x.start; e ∈ lastDay(x) • plusMonths(s, remissionMoreThanMonths) ≤ e)) ∧
(∀ v : ClusterView • (∀ i ∈ dom v.bouts • i < #v.bouts ⇒ ¬ v.bouts(i).ongoing ∧
      ∀ e ∈ v.bouts(i).end; s ∈ v.bouts(i + 1).start • e < s) ∧
   (∀ i ∈ dom v.remissions • i < #v.remissions ⇒ ¬ v.remissions(i).ongoing ∧
      ∀ e ∈ v.remissions(i).end; s ∈ v.remissions(i + 1).start • e < s)) ∧
(∀ r : ClusterAttackRate • r.rate ≥ 0 ∧ onlyOfType(ctx, r.typeScope, c3_1) ∧
   (∀ s ∈ r.bout.start • s ≤ r.period.start) ∧ (∀ e ∈ lastDay(r.bout) • r.period.end ≤ e)) ∧
(∀ v : View; p : Period; sc : TypeScope • (∃ r ∈ v.content ∩ ClusterAttackRate • r.period = p ∧ r.typeScope = sc) ⇒
   ∃ n : ℕ • (∀ e ∈ v.content ∩ AttackCount • sameSpan(e.period, spanOf(p)) ∧ e.typeScope = sc ⇒ e.count = n) ∧
     ∀ r ∈ v.content ∩ ClusterAttackRate • sameSpan(r.period, spanOf(p)) ∧ r.typeScope = sc ⇒
       (r.basis = perDay ⇒ r.rate ≈ n ÷ p.lengthDays) ∧ (r.basis = perWeek ⇒ r.rate ≈ 7 × n ÷ p.lengthDays))
```
- Reading: An ongoing period, one that has not ended by the as-of date, shows no end date, and an end date shown lies on or before the as-of date; a duration is the number of days from start to end or, while the period is ongoing, to the as-of date (its duration to date), whatever period the view covers; a remission period that shows its start date lasts more than three months, to its end or, while ongoing, to the as-of date (every fully conformant output shows the start date, E-063 `start`, SHOULD); bouts and remissions are each in chronological order, and only the last can be ongoing; an attack rate counts cluster headache attacks only (its type scope is cluster headache or a subtype of it, or all types combined for a subject who has cluster headache and neither has nor may have another headache type) and refers to a period within its bout. In one view, the attack rates of one period (periods with the same dates) and type scope rest on one whole number of attacks, which is the attack count shown for a period with those dates and that scope where the view shows one: the rate per day is that number divided by the length of the period in days, and the rate per week is seven times that.
- Conformance: definitional (E-063, E-064). Scope: output.
- Realises: OUT-031
- Evidence: Stage 1 OUT-031, OUT-029; [S-001], [S-007] INV-089/Q00.
- Notes: Relations: INV-124. See ISS-12. Rationale: INV-089/D01, INV-089/D02, INV-089/S01.

### INV-110 The dates of a trigger co-occurrence view lie in the period it covers
- Predicate:
```omn
∀ v : TriggerCooccurrenceView • ∀ d ∈ v.factorDates ∪ v.attackOnsets • inPeriod(d, v.covers)
```
- Reading: Every day on which a trigger co-occurrence view shows the potential trigger factor as present, and every attack onset it shows, lies within the reporting period the view covers.
- Conformance: definitional (E-065). Scope: output.
- Realises: OUT-001, OUT-032
- Evidence: Stage 1 OUT-001 ("Every summary output MUST state the reporting period it covers (start date, end date and length)"), OUT-032 ("the co-occurrence over time of attacks with potential trigger factors").
- Notes: Rationale: INV-110/D01, INV-110/S01.

### INV-091 No composite index as a primary measure for migraine
- Predicate:
```omn
¬ ∃ x : CompositeIndex • concerns(ctx, x.typeScope, c1) ∧ x.role = primaryRole
```
- Reading: For migraine, no composite headache index is presented as a primary measure.
- Conformance: SHOULD NOT. Scope: output.
- Realises: OUT-037
- Evidence: Stage 1 OUT-037.

### INV-092 A migraine composite index shows a component for each dimension it combines
- Predicate:
```omn
∀ x : CompositeIndex • concerns(ctx, x.typeScope, c1) ⇒
  ∀ d ∈ x.combines • ∃ m ∈ x.components • dimensionOf(m, d)
```
- Reading: If a composite index is shown for migraine, it shows a component measure for each dimension it combines.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-037
- Evidence: Stage 1 OUT-037.

### INV-115 The components of a composite index for migraine are of its period and type scope
- Predicate:
```omn
∀ x : CompositeIndex • concerns(ctx, x.typeScope, c1) ⇒ ∀ m ∈ x.components • m.period = x.period ∧ m.typeScope = x.typeScope
```
- Reading: Every component measure that a composite index for migraine shows is a value of the index's own reporting period and type scope.
- Conformance: definitional (E-033). Scope: output.
- Realises: OUT-037
- Evidence: Stage 1 OUT-037 ("If such an index is shown for migraine, it SHOULD be labelled as exploratory and shown together with its component measures").
- Notes: Rationale: INV-115/D01, INV-115/S01.

### INV-093 AUC as a primary measure for tension-type headache is shown with headache days
- Predicate:
```omn
∀ x : CompositeIndex • x.index = areaUnderHeadacheCurve ∧ concerns(ctx, x.typeScope, c2) ∧ x.role = primaryRole ⇒
  shownDay(viewOf(x), headacheDays, x.period, x.typeScope)
```
- Reading: If the area under the headache curve is presented as a primary measure for tension-type headache, headache days for the same period are shown with it.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-037
- Evidence: Stage 1 OUT-037.

### 6.11 Audience-specific views, paediatric outputs and caveats

### INV-094 Clinician-facing summary available
- Predicate:
```omn
∀ c ∈ Ctx • c.audience ∈ Clinicians ⇒
  (∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ ClinicianSummary • sameSpan(v.covers, c.timeRange)) ∧
  (∀ r ∈ c.chosenPeriod • ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ ClinicianSummary • sameSpan(v.covers, r)) ∧
  (∀ d ∈ c.previousConsultation • ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ ClinicianSummary •
     v.covers.start = d ∧ v.covers.end = c.asOf)
```
- Reading: For a clinician reader (the treating clinician with whom the summary is shared), a clinician-facing summary is available for a period chosen by the clinician, whatever its dates up to the as-of date: the period chosen for the summary (`chosenPeriod`) and the selected time range, which the clinician reader selects; and for the period since the previous consultation.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-034
- Evidence: Stage 1 OUT-034 ("for the period since the previous consultation (or a period chosen by the clinician)").
- Notes: R-MCF (3). Rationale: INV-094/D01, INV-094/S01.

### INV-095 Patient-facing overview available
- Predicate:
```omn
∀ c ∈ Ctx • c.audience ∈ {adultPatient, parentOrCaregiver} ⇒
  ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ PatientOverview • sameSpan(v.covers, c.timeRange)
```
- Reading: For a patient, parent or caregiver, a patient-facing overview of the selected time range is available.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-035
- Evidence: Stage 1 OUT-035.

### INV-096 Paediatric outputs: PedMIDAS, school days and caregiver impact
- Predicate:
```omn
∀ c ∈ Ctx •
  (∀ a ∈ c.subject.instrumentAdministrations • a.instrument = pedmidas ∧ inSpan(a.date, c.timeRange) ∧ childOn(c, a.date) ⇒
     ∃ o : Output • (c, o) ∈ Rep ∧ ∃ r ∈ parts(o) ∩ InstrumentResult • r.instrument = pedmidas ∧ r.completionDate = {a.date} ∧
       r.recallPeriod = {recallMonths(3)}) ∧
  (childOn(c, c.timeRange.from) ⇒
     ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views; sr ∈ v.content ∩ Series • tiles(sr, c.timeRange, c.granularity) ∧
       let C == {p ∈ ran sr.periods | childOn(c, p.start)} •
         ((∀ p ∈ C • ∃ m ∈ v.content ∩ fiDays(paidWorkOrSchool, affected) • m.period = p ∧ m.typeScope = allTypes) ∨
          (∀ p ∈ C • (∃ m ∈ v.content ∩ fiDays(paidWorkOrSchool, missed) • m.period = p ∧ m.typeScope = allTypes) ∧
             ∃ m ∈ v.content ∩ fiDays(paidWorkOrSchool, impaired) • m.period = p ∧ m.typeScope = allTypes)) ∧
         ∀ p ∈ C • ∃ m ∈ v.content ∩ CaregiverImpact • m.period = p ∧ m.typeScope = allTypes)
```
- Reading: Available PedMIDAS results completed within the selected time range while the subject is a child or adolescent are reported with their 3-month recall period. Where the subject is a child or adolescent on the first day of the selected time range, then for every period of the selected time range that begins while the subject is a child or adolescent, school days missed or impaired (as one count of the days on which headache affected school, or as separate counts of the days missed and the days impaired) and the impact on parents or caregivers are reported.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-036
- Evidence: Stage 1 OUT-036 (a), (b).
- Notes: R-MCF (4). Rationale: INV-096/D01.

### INV-097 Paediatric comparisons use periods of equal length
- Predicate:
```omn
(∀ pc : PeriodComparison • childIn(ctx, ran pc.periods) ⇒ equalLengths(ran pc.periods)) ∧
(∀ rc : ResponseComparison • childIn(ctx, {rc.baseline} ∪ ran rc.onTreatment) ⇒ equalLengths({rc.baseline} ∪ ran rc.onTreatment)) ∧
(∀ v : TreatmentReviewView • childIn(ctx, {v.baseline} ∪ ran v.onTreatment) ⇒ equalLengths({v.baseline} ∪ ran v.onTreatment)) ∧
(∀ v : PostStopMonitoringView • childIn(ctx, v.baseline ∪ v.onTreatmentPeriod ∪ ran v.after) ⇒
   equalLengths(v.baseline ∪ v.onTreatmentPeriod ∪ ran v.after)) ∧
(∀ ch : Change • childIn(ctx, {ch.reference.period, ch.compared.period}) ⇒ equalLengths({ch.reference.period, ch.compared.period}))
```
- Reading: Where the subject is a child or adolescent on the first day of one of the periods compared in one comparison, these periods have equal length: the periods of a period comparison, the baseline and on-treatment periods of a response comparison and of the treatment review view, the baseline, on-treatment and post-event periods of the post-stop monitoring view, and the reference and compared periods of every change.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-036
- Evidence: Stage 1 OUT-036 (c) ("apply equal-length period comparisons as in OUT-001"); OUT-021 ("present together, for the same pre-treatment baseline and on-treatment periods"), OUT-022 ("compare it with both the on-treatment period and the original pre-treatment baseline") and OUT-018 ("the absolute and percentage change from baseline") for the comparisons that these views and changes make.
- Notes: Rationale: INV-097/D01, INV-097/S01.

### INV-102 Treatment review view available for each preventive treatment
- Predicate:
```omn
∀ c ∈ Ctx; t ∈ c.subject.preventiveTreatments • startOf(c, t) ≠ ∅ ⇒
  ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ TreatmentReviewView • v.treatment = t
```
- Reading: For each preventive treatment whose start the context states, a treatment review view is available.
- Conformance: MUST. Scope: repertoire.
- Realises: OUT-021
- Evidence: Stage 1 OUT-021.
- Notes: R-MCF (1).

### INV-103 Post-stop monitoring available after a stop, pause or reduction
- Predicate:
```omn
∀ c ∈ Ctx; e ∈ c.subject.courseEvents • e.treatment ∈ c.subject.preventiveTreatments ∧
  (e.kind is stop ∨ e.kind = doseChange(reduction)) ⇒
    ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ PostStopMonitoringView • v.treatment = e.treatment ∧ v.event = e.kind ∧ v.eventDate = e.date
```
- Reading: After each stop, pause or dose reduction of a preventive treatment, whether or not the context states the start of its course, the post-stop monitoring view is available.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-022
- Evidence: Stage 1 OUT-022.
- Notes: R-MCF (2). Rationale: INV-103/D01, INV-103/S01.

### INV-104 Clinician-facing summary content
- Predicate:
```omn
∀ v : ClinicianSummary • concise ∈ v.qualities ∧
  shownDay(v, headacheDays, v.covers, allTypes) ∧ (hasType(ctx, c1) ⇒ shownDay(v, migraineDays, v.covers, allTypes)) ∧
  shownDay(v, moderateSevereHeadacheDays, v.covers, allTypes) ∧ (∃ e ∈ v.content ∩ AttackCount • e.period = v.covers ∧ e.typeScope = allTypes) ∧
  shownDay(v, headacheFreeDays, v.covers, allTypes) ∧ shownDay(v, symptomFreeDays, v.covers, allTypes) ∧
  (0 ∈ daysOf(v, migraineDays, v.covers, allTypes) ⇒
     ∃ mk ∈ v.content ∩ MigraineFreePeriodMark • mk.period = v.covers ∧ mk.typeScope = allTypes) ∧
  ((∃ g ∈ MonthlyKind • containsPeriodOf(spanOf(v.covers), g)) ⇒
   ∃ sr ∈ v.content ∩ Series • sr.granularity ∈ MonthlyKind ∧ fillsPeriod(sr, v.covers) ∧ summaryTimeCourse(v, sr) ∧
     ∀ p ∈ ran sr.periods • ∀ s ∈ {m ∈ ctx.subject.acuteMedications • ofClassUse(classOf(m.drug))} ∪ {combinedUse} •
       ∃ i ∈ v.content ∩ MedicationOveruseIndicator • i.period = p ∧ i.scope = s) ∧
  ((¬ ∃ g ∈ MonthlyKind • containsPeriodOf(spanOf(v.covers), g)) ∧ containsPeriodOf(spanOf(v.covers), calendarWeek) ⇒
   ∃ sr ∈ v.content ∩ Series • sr.granularity = calendarWeek ∧ fillsPeriod(sr, v.covers) ∧ summaryTimeCourse(v, sr)) ∧
  (∀ e ∈ ctx.subject.courseEvents • e.treatment ∈ ctx.subject.preventiveTreatments ∧ markedKind(e.kind) ∧ inPeriod(e.date, v.covers) ⇒
     ∃ mk ∈ v.content ∩ TreatmentMarker • mk.treatment = e.treatment ∧ mk.event = e.kind ∧ mk.date = e.date) ∧
  shownDay(v, acuteMedicationDays(allAcuteMedication), v.covers, allTypes) ∧
  (∀ m ∈ ctx.subject.acuteMedications • shownDay(v, acuteMedicationDays(ofClass(classOf(m.drug))), v.covers, allTypes) ∧
     shownDay(v, acuteMedicationDays(ofDrug(m.drug)), v.covers, allTypes)) ∧
  (containsPeriodOf(spanOf(v.covers), calendarWeek) ⇒
   ∃ sr ∈ v.content ∩ Series • sr.granularity = calendarWeek ∧ fillsPeriod(sr, v.covers) ∧
     perPeriod(v, sr, TotalAcuteMedicationDays, allTypes)) ∧
  (∀ t ∈ ctx.subject.preventiveTreatments • startOf(ctx, t) ≠ ∅ ⇒
     ∃ rc ∈ v.content ∩ ResponseComparison • rc.treatment = t ∧ ∃ a ∈ v.content ∩ AdherenceSummary • adherenceFor(a, rc)) ∧
  (∀ m ∈ ctx.subject.acuteMedications • ∃ s ∈ v.content ∩ AcuteTreatmentSummary • summarisesMedication(s, m) ∧ s.period = v.covers ∧
     s.typeScope = allTypes) ∧
  (∀ t ∈ ctx.subject.preventiveTreatments ∪ ctx.subject.acuteTreatments • ∃ l ∈ v.content ∩ TreatmentLine • l.treatment = t) ∧
  (∀ a ∈ ctx.subject.instrumentAdministrations • inPeriod(a.date, v.covers) ⇒
     ∃ r ∈ v.content ∩ InstrumentResult • r.instrument = a.instrument ∧ r.completionDate = {a.date}) ∧
  (∀ d ∈ {paidWorkOrSchool, householdWork, socialOrLeisure} •
     ∃ m ∈ v.content ∩ fiDays(d, affected) • m.period = v.covers ∧ m.typeScope = allTypes) ∧
  (∃ m ∈ v.content ∩ DayCount • m.period = v.covers ∧ m.typeScope = allTypes ∧
     ∃ d : ImpactDomain • m.measure = functionalImpactDays((d, severelyImpaired)))
```
- Reading: The clinician-facing summary is concise and brings together, for the period it covers: the frequency measures (headache days, migraine days for patients with migraine, moderate/severe headache days, headache-free and symptom-free days, attacks, and the mark of the covered period where it shows 0 migraine days) and their time course, with a marker for every start, dose change and stop of a preventive treatment within the covered period. The time course shows headache days, migraine days (for patients with migraine), moderate/severe headache days and attacks for every period of a series that consists of all whole periods of its granularity within the covered period (28-day periods counted from its first day), and marks every period of that series that shows 0 migraine days: a series of calendar months or 28-day periods when the covered period has at least 28 days, otherwise a series of calendar weeks when it contains a whole calendar week. The summary also shows acute-medication days in total, by class and by drug, and, for every period of its monthly series, the medication-overuse indicators of each class of the subject's acute medications and of combined use; acute-medication days for every whole calendar week within the covered period; the response comparison of each preventive treatment whose start the context states, with the adherence over an evaluation window of that comparison (`adherenceFor`, E-047), the effectiveness of each acute medication over all headache types combined in the period the summary covers (a summary of all formulations of its drug or of its own formulation, `summarisesMedication`, E-051), and a treatment line for each treatment, which shows the response of the treatment's course (INV-109); the instrument results completed within the covered period; and functional impact over all headache types combined (days affected in each of the three domains and days with severe functional impairment).
- Conformance: SHOULD. Scope: output.
- Realises: OUT-034, OUT-039
- Evidence: Stage 1 OUT-034 ("a concise clinician-facing summary for the period since the previous consultation (or a period chosen by the clinician)", "frequency measures and their time course (OUT-004 to OUT-009)", "acute medication use and any medication-overuse indicator (OUT-014 to OUT-016)", "functional impact (OUT-027)"), OUT-009 ("frequency measures (OUT-004 to OUT-007) as a time series of consecutive reporting periods"), OUT-001 ("Frequency outputs MUST be available per calendar month or per 28-day (4-week) period"), OUT-015 ("acute medication days per calendar week"), OUT-016 ("per reporting period"), OUT-027 ("including days with severe functional impairment"), OUT-039 ("The adherence output SHOULD also be available [...] in the clinician-facing summary (OUT-034)").
- Notes: See ISS-04. R-MCF (1), (3), (4). Rationale: INV-104/D01, INV-104/S01.

### INV-105 Patient-facing overview content
- Predicate:
```omn
∀ v : PatientOverview • plainLanguage ∈ v.qualities ∧
  shownDay(v, headacheDays, v.covers, allTypes) ∧ shownDay(v, migraineDays, v.covers, allTypes) ∧
  (∃ m ∈ v.content ∩ IntensitySummary • m.period = v.covers ∧ m.typeScope = allTypes) ∧
  shownDay(v, acuteMedicationDays(allAcuteMedication), v.covers, allTypes) ∧
  ((∃ g : Granularity • containsPeriodOf(spanOf(v.covers), g)) ⇒
   ∃ sr ∈ v.content ∩ Series • fillsPeriod(sr, v.covers) ∧
     perPeriod(v, sr, HeadacheDays, allTypes) ∧ perPeriod(v, sr, MigraineDays, allTypes) ∧
     (∃ i₁ ∈ v.content ∩ IntensitySummary • perPeriod(v, sr, {m : IntensitySummary | onSameScale(m, i₁)}, allTypes)) ∧
     perPeriod(v, sr, TotalAcuteMedicationDays, allTypes)) ∧
  ((∃ t ∈ ctx.subject.preventiveTreatments • courseOverlaps(ctx, t, v.covers)) ∨
   (∃ t ∈ ctx.subject.acuteTreatments • courseNotOutside(ctx, t, v.covers)) ⇒
     (∃ rc ∈ v.content ∩ ResponseComparison • courseOverlaps(ctx, rc.treatment, v.covers)) ∨
     ∃ s ∈ v.content ∩ AcuteTreatmentSummary; m ∈ ctx.subject.acuteMedications • s.typeScope = allTypes ∧
       summarisesMedication(s, m) ∧ within(s.period, v.covers) ∧
       ∃ t ∈ ctx.subject.acuteTreatments • drugOf(t) = m.drug ∧ courseNotOutside(ctx, t, s.period)) ∧
  (menstruatesDuring(ctx, spanOf(v.covers)) ⇒ ∃ cl ∈ v.content ∩ CycleLine • cl.cycle.from ≤ v.covers.end ∧ v.covers.start ≤ cl.cycle.to)
```
- Reading: The patient-facing overview, in plain language, shows the patient's headache pattern over time: headache days, migraine days, intensity and acute-medication days for the period it covers and, where that period contains at least one whole calendar month, 28-day period or calendar week, for every period of a series that consists of all whole periods of its granularity within the covered period (28-day periods counted from its first day), with the intensity of the periods of the series on one scale and in one form (`onSameScale`, E-023), so that its course over time can be followed. It also shows the effect of the patient's treatment (the response comparison of a preventive treatment taken during the period the overview covers, whose stated start lies on or before the end of that period and has not stopped before it begins, or an acute-treatment summary over all headache types combined of the period the overview covers or of a period within it, of an acute medication the subject has used, of all formulations of its drug or of its own formulation, whose drug is that of an acute treatment course taken during the summary's period: a course that has not started after the last day of that period and has not stopped before its first day, a course whose start the context does not state counting as started) where the patient has a preventive treatment taken during the period the overview covers or an acute treatment course that the context does not place outside that period, and, where the subject menstruates during the period the overview covers, the relationship to menstruation: a cycle line that overlaps that period.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-035
- Evidence: Stage 1 OUT-035 ("an understandable overview of their own headache pattern over time (headache and migraine days, intensity, acute medication use, treatment effect and, where relevant, the relationship to menstruation)", "so that patients can follow the effect of their treatment and prepare consultations").
- Notes: See ISS-03. R-MCF (1), (2). Rationale: INV-105/D01, INV-105/D02, INV-105/D03, INV-105/D04, INV-105/D05, INV-105/S01, INV-105/S02.

### 6.12 Decisions left to the reader

All invariants of this subsection were merged into the generic invariants of section 6.0 (section 9).

## 7. Traceability

Every Stage 1 requirement, in Stage 1 order (OUT-039 follows OUT-025), with its strength by statement part, the catalogue rows, elements and invariants that realise it (from their Realises fields), and its coverage: "full" when every observable property of the Statement, and every Caveat that constrains what an output shows, is represented, with one line per statement part: "<part> (<level>): <items>".

| Requirement | Strength (Stage 1, by part) | Catalogue rows | Elements | Invariants | Coverage |
|---|---|---|---|---|---|
| OUT-001 | MUST | OC-01, OC-02, OC-05, OC-06, OC-07, OC-08, OC-21, OC-33, OC-38 | E-002, E-003, E-005, E-006, E-007, E-012, E-015, E-016, E-017, E-019, E-037, E-043 | INV-001, INV-002, INV-003, INV-004, INV-037, INV-038, INV-055, INV-110, INV-118, INV-121 | full<br>reporting period of every summary output, with start, end and length (MUST): E-003, E-005, INV-002, INV-003, INV-110<br>frequency outputs per calendar month or 28-day period (MUST): INV-118 (C1-01, C1-02, C1-04, C1-06); section 3.4<br>comparison of periods of equal length (MUST): E-037, INV-037, INV-038; baseline and on-treatment periods, INV-055<br>Caveat (days of each calendar month visible): E-005 `lengthDays` |
| OUT-002 | SHOULD | OC-03, OC-05, OC-06, OC-07, OC-08 | E-011, E-015, E-016, E-017, E-019 | INV-008, INV-111 | full<br>definition label for each defined measure reported (SHOULD): E-011, INV-008 (`reports`)<br>one definition per measure (definitional): INV-111 |
| OUT-003 | SHOULD; SHOULD NOT | OC-04 | E-001, E-013 | INV-011, INV-012, INV-119, INV-121 | full<br>completeness indicator next to the summary measures of each reporting period (SHOULD): E-013, INV-011, INV-012, INV-121<br>no completeness cut-off presented as clinically validated (SHOULD NOT): INV-119 (C2-02) |
| OUT-004 | MUST | OC-02, OC-03, OC-05 | E-006, E-007, E-011, E-014, E-015 | INV-001, INV-004, INV-006, INV-118, INV-121, INV-125 | full<br>headache days for every period of the selected time range (MUST): E-006, E-015, INV-004, INV-118 (C1-01)<br>"headache days" as defined in ICHD-3 (MUST): INV-125 (SD-DF-01) |
| OUT-005 | MUST; SHOULD (label) | OC-03, OC-06 | E-008, E-009, E-011, E-014, E-016 | INV-008, INV-118, INV-121 | full<br>migraine days per reporting period for patients with migraine (MUST): E-016, INV-118 (C1-02)<br>definition label (SHOULD): INV-008 |
| OUT-006 | SHOULD | OC-03, OC-07 | E-011, E-014, E-017 | INV-008, INV-118, INV-121, INV-122 | full<br>moderate/severe headache days per reporting period (SHOULD): E-017, INV-118 (C1-03); where provided, per calendar month or 28-day period (MUST, OUT-001): INV-118 (C1-04)<br>definition named (SHOULD): INV-008; nesting: INV-122 |
| OUT-007 | SHOULD | OC-03, OC-08 | E-011, E-019 | INV-006, INV-008, INV-118, INV-125 | full<br>attacks per reporting period, separately from days (SHOULD): E-019, INV-118 (C1-05); where provided, per calendar month or 28-day period (MUST, OUT-001): INV-118 (C1-06)<br>"frequency of attacks" as defined in ICHD-3 (SHOULD): INV-125 (SD-DF-02) |
| OUT-008 | MAY | OC-09, OC-44 | E-010, E-014, E-020, E-021, E-022 | INV-031, INV-120, INV-121, INV-122 | full<br>headache-free days, symptom-free days, periods without migraine days, as exploratory measures (MAY): E-020, E-021, E-022, C3-02; relations INV-031, INV-122; in the clinician-facing summary (SHOULD, OUT-034): INV-104 (ISS-04) |
| OUT-009 | SHOULD | OC-02, OC-10 | E-006, E-007, E-008, E-034, E-035 | INV-001, INV-004, INV-034, INV-035, INV-123 | full<br>time series of consecutive periods with dated markers of preventive treatments (SHOULD): E-006, E-034, E-035, INV-034, INV-035, W2 (E-035), INV-123<br>weekly values where weekly granularity is clinically relevant (SHOULD): INV-034 (`weeklyGranularityRelevant`, E-007; INV-001) |
| OUT-010 | SHOULD | OC-11, OC-33 | E-023, E-037 | INV-032, INV-039, INV-118, INV-121 | full<br>intensity per reporting period on a stated scale (SHOULD): E-023, INV-118 (C1-07), INV-032<br>comparison between periods (SHOULD): E-037, INV-039 |
| OUT-011 | SHOULD; Caveat SHOULD | OC-12, OC-44 | E-001, E-010, E-024 | INV-118, INV-119, INV-120, INV-121 | full<br>duration per reporting period (SHOULD): E-024, INV-118 (C1-08), INV-121<br>label of durations of acutely treated attacks (SHOULD): INV-120 (C3-03)<br>Caveat, not a stand-alone efficacy measure (SHOULD NOT): INV-119 (C2-03) |
| OUT-012 | SHOULD | OC-13, OC-28 | E-008, E-009, E-025, E-026, E-050, E-051, E-053 | INV-033, INV-072, INV-075, INV-076, INV-118, INV-121, INV-123 | full<br>associated symptoms and most bothersome symptom across periods, for migraine (SHOULD): E-025, E-026, INV-118 (C1-09), INV-033<br>in the response of individual treated attacks (SHOULD): E-053, INV-076; in the treatment review view: INV-069 |
| OUT-013 | MAY | OC-12, OC-14 | E-008, E-009, E-019, E-024, E-027 |  | full<br>auras per reporting period and their duration, separately from headache measures, for migraine with aura (MAY): E-019, E-024, E-027 |
| OUT-014 | MUST | OC-15, OC-17 | E-008, E-009, E-014, E-028, E-029, E-032 | INV-001, INV-024, INV-118, INV-121, INV-122, INV-123 | full<br>acute-medication days per reporting period, by ICHD-3 8.2 class, by drug and in total (MUST): E-028, E-029, INV-118 (C1-10), SD-CLS<br>relations of totals, classes and drugs (definitional): INV-024, INV-122; medication used (definitional): INV-123 |
| OUT-015 | SHOULD | OC-02, OC-15, OC-16 | E-006, E-029, E-036 | INV-118, INV-121 | full<br>acute-medication days per calendar week (SHOULD): E-036, INV-118 (C1-11) |
| OUT-016 | MUST; MUST NOT | OC-15, OC-17, OC-44 | E-001, E-008, E-009, E-010, E-028, E-029, E-032 | INV-024, INV-044, INV-045, INV-046, INV-119, INV-120, INV-122, INV-123 | full<br>indicator per reporting period, per class and for combined use, against the levels and time span of ICHD-3 8.2 (MUST): E-032, INV-044, INV-045, INV-046, SD-CLS, SD-CMB, SD-FX-06<br>worded as a prompt for clinical review (MUST): INV-120 (C3-04)<br>not presented as a diagnosis of medication-overuse headache (MUST NOT): INV-119 (C2-04) |
| OUT-017 | SHOULD | OC-18, OC-44 | E-008, E-010, E-039 | INV-049, INV-050, INV-051, INV-120, INV-123 | full<br>headache days and acute-medication days from the start of withdrawal, with the NICE CG150 1.3.48 review window (SHOULD): E-039, INV-049, INV-050, INV-051, W2 (E-039), SD-FX-03, SD-FX-04<br>continued monitoring over the following year (SHOULD): INV-049, SD-FX-05<br>label of the expected transient worsening (SHOULD): INV-120 (C3-06)<br>start of withdrawal of the subject (definitional): INV-123 |
| OUT-018 | MUST; Caveat MUST | OC-19, OC-20, OC-21 | E-001, E-008, E-040, E-041, E-042, E-043, E-045 | INV-001, INV-053, INV-055, INV-056, INV-057, INV-058, INV-059, INV-119, INV-123 | full<br>comparison of monthly migraine days and headache days (and, where reported, moderate/severe headache days) between a pre-treatment baseline and periods after the start, aligned to the start, with the values and the absolute and percentage change (MUST): E-040, E-043, INV-053, INV-055, INV-056, INV-057, W2 (E-040), INV-123<br>at the evaluation time points of current guidance (MUST): E-041, E-042, SD-ER, INV-055, INV-058, INV-059, W2 (E-043)<br>Caveat, no decision on continuation (MUST NOT): INV-119 (C2-05) |
| OUT-019 | SHOULD | OC-19, OC-22 | E-040, E-044 | INV-060, INV-061, INV-062 | full<br>residual burden next to a percentage change in migraine or headache days (SHOULD): E-044, INV-060, INV-061; compared periods shorter than 28 days: ISS-13 |
| OUT-020 | MAY (label); SHOULD; SHOULD NOT | OC-19, OC-23, OC-24, OC-31 | E-001, E-008, E-012, E-014, E-018, E-040, E-045, E-046, E-058 | INV-031, INV-062, INV-063, INV-064, INV-114, INV-116, INV-119, INV-120, INV-123 | full<br>responder or non-responder label (MAY): E-046<br>criterion named, underlying values and other values the criterion rests on (SHOULD): E-018, E-045, INV-062, W2 (E-046), SD-RC, SD-CL; definitional: INV-063, INV-064, INV-114, INV-116, INV-123<br>not the sole indicator of individual benefit (SHOULD NOT): INV-119 (C2-06); clinical interpretation (OUT-038): INV-120 (C3-07) |
| OUT-021 | MUST; SHOULD (further components) | OC-11, OC-13, OC-26, OC-28, OC-31 | E-008, E-023, E-025, E-026, E-048, E-051, E-058 | INV-068, INV-069, INV-071, INV-072, INV-102, INV-123 | full<br>headache days, migraine days and acute-medication days together for the same baseline and on-treatment periods (MUST): E-048, INV-102, INV-068<br>further components where provided (SHOULD): INV-069 |
| OUT-022 | SHOULD | OC-27 | E-008, E-049 | INV-001, INV-070, INV-103, INV-112, INV-123 | full<br>frequency after a stop, pause or reduction, compared with the on-treatment period and the original baseline (SHOULD): E-049, INV-103, INV-070, INV-112, INV-123 |
| OUT-023 | SHOULD; Caveat SHOULD | OC-26, OC-28 | E-001, E-008, E-012, E-050, E-051, E-052, E-053 | INV-069, INV-071, INV-072, INV-073, INV-074, INV-075, INV-119, INV-123 | full<br>outcome measures per acute medication, their consistency across treated attacks, relief, non-pain symptoms, adverse events, intake timing, formulation, per formulation (SHOULD): E-050, E-051, E-052, E-053, SD-ET, INV-071, INV-072, INV-073, INV-074, INV-075, W2 (E-051), INV-123<br>Caveat, no decision on the definition of response (SHOULD NOT): INV-119 (C2-07) |
| OUT-024 | SHOULD | OC-28, OC-29 | E-008, E-051, E-054, E-055 | INV-001, INV-077, INV-078, INV-079, INV-109, INV-123 | full<br>chronological list of preventive and acute treatments, grouped by class, with dates, dose changes, duration, response summary, adverse effects, reason for stopping and formulation (SHOULD): E-054, E-055, INV-077, INV-078, INV-079, INV-109, W2 (E-054, E-055), INV-123 |
| OUT-025 | MAY | OC-23, OC-30, OC-31 | E-007, E-046, E-056, E-058 | INV-080 | full<br>evaluation windows of a scheme, labelled with the scheme (MAY): E-056, INV-080 |
| OUT-039 | SHOULD | OC-25, OC-29, OC-40 | E-008, E-047, E-054, E-055, E-066 | INV-066, INV-067, INV-079, INV-104, INV-109, INV-123 | full<br>adherence over the evaluation window next to the response comparison (SHOULD): E-047, INV-066, INV-067, INV-123<br>in the treatment history and the clinician-facing summary (SHOULD): INV-109, W2 (E-055), INV-104 |
| OUT-026 | SHOULD | OC-31 | E-008, E-057, E-058 | INV-081, INV-082, INV-120, INV-123 | full<br>results of validated instruments where available, with name, date, recall period, score, grading and change from baseline (SHOULD): E-057, E-058, SD-IN, SD-GB, INV-081, INV-082, INV-123; clinical interpretation of categories (OUT-038): INV-120 (C3-08) |
| OUT-027 | SHOULD | OC-32, OC-33 | E-014, E-030, E-037 | INV-027, INV-118, INV-121, INV-122 | full<br>functional impact per reporting period, with severe impairment (SHOULD): E-030, INV-118 (C1-12), INV-121, INV-122<br>comparison with the baseline period (SHOULD): INV-027 |
| OUT-028 | MUST; SHOULD; SHOULD NOT | OC-02, OC-03, OC-34 | E-001, E-006, E-009, E-011, E-038 | INV-008, INV-040, INV-041, INV-042, INV-119 | full<br>three-month view of headache days and migraine days (MUST): E-038, INV-040, INV-041, W2 (E-038)<br>source definitions shown (SHOULD): INV-042<br>no diagnosis assigned (SHOULD NOT): INV-119 (C2-08) |
| OUT-029 | MUST; SHOULD (intensity) | OC-11, OC-15, OC-35 | E-008, E-009, E-012, E-023, E-029 | INV-001, INV-118, INV-122 | full<br>frequency and acute-medication outputs per headache type and combined (MUST): E-012, INV-118 (C1-13); values per type do not exceed the combined values: INV-122<br>intensity per headache type where provided (SHOULD): INV-118 (C1-14) |
| OUT-030 | MUST | OC-36 | E-008, E-060, E-061 | INV-086, INV-087, INV-124 | full<br>migraine attacks and migraine days in relation to menstruation across consecutive cycles, with the ICHD-3 A1.1 perimenstrual window, and the number of complete cycles (MUST): E-060, E-061, INV-086, INV-087, INV-124, W2 (E-060), SD-FX-01, SD-FX-02 |
| OUT-031 | SHOULD | OC-28, OC-37 | E-008, E-009, E-012, E-050, E-051, E-052, E-062, E-063, E-064 | INV-072, INV-073, INV-088, INV-089, INV-124 | full<br>cluster periods and remission periods with dates and durations, attacks per day and per week, acute effectiveness at 15 minutes and rescue, previous bouts (SHOULD): E-062, E-063, E-064, INV-088, INV-089, INV-124, SD-FX-07, SD-ET-01 |
| OUT-032 | MAY; caveats SHOULD | OC-38, OC-44 | E-010, E-065 | INV-110, INV-120 | full<br>co-occurrence of attacks with trigger factors (MAY): E-065, INV-110<br>caveats (SHOULD): INV-120 (C3-09) |
| OUT-033 | SHOULD; Caveat SHOULD | OC-39 | E-001, E-008, E-059 | INV-083, INV-085, INV-119, INV-120, INV-123 | full<br>screening results where available, with name, date and score, next to the headache outputs (SHOULD): E-059, SD-SC, SD-SR, INV-083, INV-085, INV-123<br>Caveat, not psychiatric diagnoses (SHOULD NOT): INV-119 (C2-09); clinical interpretation: INV-120 (C3-10) |
| OUT-034 | SHOULD | OC-01, OC-04, OC-10, OC-29, OC-31, OC-40 | E-003, E-007, E-035, E-058, E-066 | INV-001, INV-011, INV-094, INV-104, INV-109 | full<br>concise clinician-facing summary for the period since the previous consultation or a chosen period, with the outputs listed (SHOULD): E-003 (`concise`), E-066, INV-094, INV-104 |
| OUT-035 | SHOULD | OC-01, OC-10, OC-11, OC-36, OC-41 | E-003, E-007, E-008, E-023, E-035, E-060, E-067 | INV-087, INV-095, INV-105, INV-124 | full<br>patient-facing overview in plain language, with the components listed (SHOULD): E-003 (`plainLanguage`), E-067, INV-095, INV-105 |
| OUT-036 | SHOULD; Caveat SHOULD | OC-19, OC-20, OC-21, OC-26, OC-27, OC-31, OC-32, OC-33, OC-42, OC-44 | E-007, E-008, E-010, E-030, E-031, E-037, E-040, E-041, E-043, E-048, E-049, E-057, E-058 | INV-055, INV-082, INV-096, INV-097, INV-120, INV-121, INV-122, INV-123 | full<br>(a) PedMIDAS with its recall period, (b) school days and caregiver impact (SHOULD): E-030, E-031, E-058, INV-096<br>(c) equal-length comparisons (SHOULD): INV-097<br>(d) efficacy as in paediatric guidance (SHOULD): E-041 (SD-ER-15), INV-055<br>Caveat, supportive information (SHOULD): INV-120 (C3-11) |
| OUT-037 | SHOULD NOT; SHOULD; SHOULD | OC-43, OC-44 | E-008, E-009, E-010, E-012, E-033 | INV-091, INV-092, INV-093, INV-115, INV-120 | full<br>composite index not a primary measure for migraine (SHOULD NOT): E-033, INV-091<br>exploratory label and component measures for migraine (SHOULD): INV-120 (C3-12), W2 (E-033), INV-092, INV-115<br>headache days with AUC for tension-type headache (SHOULD): INV-093 |
| OUT-038 | SHOULD | OC-01, OC-17, OC-23, OC-31, OC-34, OC-38, OC-39, OC-44, OC-45 | E-001, E-002, E-003, E-004, E-010, E-032, E-038, E-046, E-058, E-059, E-065 | INV-119, INV-120 | full<br>patient-reported information; supports but does not replace clinical assessment (SHOULD): INV-120 (C3-01); not presented as replacing assessment or as a diagnosis (SHOULD NOT): INV-119 (C2-01)<br>indicators, labels and associations require clinical interpretation (SHOULD): INV-120 (C3-05, C3-07, C3-08, C3-09, C3-10); other content: E-004, E-010 |

## 8. Stage 1 issues for the human

The model follows Stage 1 in each case below. Each issue is pointed to from the Notes of the elements it affects. The verbatim quotes of each issue are in the `RATIONALE.md` entries that its Evidence field names.

### ISS-01 The basis of the ICHD-3 8.2.6 indicator is not the total across all classes
- Stage 1: OUT-016 asks for the indicator "for ICHD-3 subtype 8.2.6, for the combined use of acute medication across classes (see the total across classes in OUT-014)". The total of OUT-014 is the total across all acute-medication classes, including combination analgesics and "other classes".
- Evidence: [S-001] ISS-01/Q00.
- Effect on the model: so that the indicator relation is correct under ICHD-3 (Stage 2 PROCESS.md section 2), the basis of the 8.2.6 indicator is the days with any medication of the classes ICHD-3 names (`ofClasses(classesOf826)`, E-028, E-029, E-032), not the OUT-014 total. Whether days with combination-analgesic intake belong to that total is not stated explicitly by ICHD-3; the shown basis states the classes it covers.
- For the human: confirm that the 8.2.6 indicator rests on the classes named in ICHD-3 8.2.6 criterion B rather than on the OUT-014 total.

### ISS-02 "Simple analgesics" is not the ICHD-3 name of the class
- Stage 1: OUT-014 gives as an example of the ICHD-3 8.2 drug classes "ergotamine, triptans, simple analgesics, opioids, combination analgesics, and other classes".
- Evidence: [S-001] ISS-02/Q00.
- Effect on the model: the class is named by its ICHD-3 subtype label (E-028). The example in OUT-014 is not a requirement, so the model is not narrowed.
- For the human: consider correcting the example label in Stage 1 to the ICHD-3 class name, non-opioid analgesics; the one use of "simple analgesics" in ICHD-3 (above) refers to drugs of that class, which indicates the class that the Stage 1 example means.

### ISS-03 Migraine days without the "patients with migraine" condition
- Stage 1: OUT-005 reports migraine days "for patients with migraine". OUT-008 ("periods without migraine days", MAY), OUT-018 ("monthly migraine days and monthly headache days"), OUT-019 ("the absolute number of migraine days and moderate/severe headache days per month that remain on treatment", next to "a relative (percentage) change in migraine or headache days"), OUT-022 ("headache and migraine frequency"), OUT-028 ("headache days and migraine days"), OUT-030 ("migraine attacks and migraine days in relation to the days of menstruation", MUST, whose only stated condition is "For patients who menstruate") and OUT-035 ("headache and migraine days") name migraine days without that condition and without a reference to OUT-005. OUT-009, OUT-021 and OUT-034 refer to OUT-005 by its ID, and OUT-020 refers to OUT-018 and OUT-019 by theirs ("the underlying values (OUT-018, OUT-019)"). OUT-002 and OUT-007 name migraine days but require none: OUT-002 asks outputs that report them to state their definition, and OUT-007 asks for attacks "separately from the number of headache or migraine days".
- Evidence: [S-001] ISS-03/Q00.
- Effect on the model: by the reference rule of section 3.5, components that refer to OUT-005 by ID keep its condition (INV-035, INV-068, INV-104). Components named without the reference are modelled as stated, without the condition (INV-040, INV-056, INV-070, INV-105). The same holds for:
  - OUT-008 (MAY): a mark of a period without migraine days is permitted for every subject (E-022), and the clinician-facing summary marks its covered period and each period of its time course for which it shows 0 migraine days (INV-104; ISS-04);
  - OUT-019: residual migraine days next to every percentage change in migraine or headache days whose compared period has at least 28 days (ISS-13), whatever the subject's headache types (E-044, INV-060, INV-061), and with a responder label, which shows the residual burden by its reference to OUT-019 (INV-062);
  - OUT-030 (MUST): the menstrual-relation view, with the migraine days and migraine attacks of each cycle line, for every selected time range during which the subject menstruates, whether or not the subject has migraine (E-060, E-061, INV-086, INV-087); the cycle lines of the patient-facing overview have the same content (INV-105).

  For a subject without migraine (for example a preventive treatment for tension-type headache, or a subject who menstruates and has only tension-type headache), these outputs show no migraine days (counts of 0) and no migraine attacks.
- For the human: decide whether migraine-day components of OUT-008, OUT-018, OUT-019, OUT-022, OUT-028 and OUT-035, and the menstrual-relation view of OUT-030, which is MUST, apply only to patients who have (or, for OUT-028 and OUT-030, which Stage 1 groups among the outputs that support diagnosis and classification, may have) migraine.

### ISS-04 The clinician-facing summary includes MAY measures at SHOULD level, and the frequency outputs of OUT-001
- Stage 1: OUT-034 (SHOULD) brings together "frequency measures and their time course (OUT-004 to OUT-009)". The range includes OUT-008 (headache-free days, symptom-free days, periods without migraine days), which is MAY in its own requirement. OUT-009 instead names "frequency measures (OUT-004 to OUT-007)", and OUT-008 calls its own measures "exploratory measures of residual burden". OUT-001 (MUST) requires "Frequency outputs" to be available per calendar month or per 28-day period without saying which outputs these are.
- Effect on the model: each part keeps its own strength (Stage 2 PROCESS.md section 4), so INV-104 includes headache-free days, symptom-free days and the marks of periods without migraine days in the clinician-facing summary at SHOULD. A diary that provides no OUT-008 measures at all, as OUT-008 permits, then deviates from the SHOULD of OUT-034. The frequency outputs of OUT-001 are read as the frequency measures of OUT-004 to OUT-007, as OUT-009 names them (section 3.4). So the MUST of OUT-001 makes headache days, migraine days for patients with migraine, and, where provided, moderate/severe headache days and attacks available per calendar month or 28-day period (INV-118 (C1-01, C1-02, C1-04, C1-06)). It does not do so for the OUT-008 measures or for the aura counts of OUT-013, which keep "per reporting period" at MAY.
- For the human: decide whether OUT-034 means OUT-008 measures "where provided"; and whether the frequency outputs of OUT-001 also include the OUT-008 measures (and the aura counts of OUT-013), which would make their availability per calendar month or 28-day period MUST wherever the diary provides them.

### ISS-05 OUT-019 and the single count of the IHS position statement 2025
- Stage 1: OUT-019 asks for "the absolute number of migraine days and moderate/severe headache days per month that remain on treatment", citing [S-010]. OUT-020 names the "IHS position statement 2025 control levels" as a criterion.
- Evidence: [S-010] ISS-05/Q00.
- Effect on the model: OUT-019 is modelled as two counts (migraine days and moderate/severe headache days, E-044). The single count of [S-010] is modelled only as the value on which control-level labels rest (E-018, INV-062, INV-064), because OUT-020 requires the values a named criterion rests on.
- For the human: decide whether OUT-019's residual burden should also, or instead, show the single count of [S-010].

### ISS-06 "Total score" for instruments that have none
- Stage 1: OUT-026 asks for the "total score" of every validated instrument and names HURT and PGIC among them.
- Evidence: [S-008], [S-014] ISS-06/Q00.
- Effect on the model: `totalScore` is SHOULD for every instrument as Stage 1 states it (E-058); categories are shown as published (`publishedCategory`). For HURT the SHOULD cannot be met, and the change from the baseline administration, which INV-082 relates to the total scores, then has no defined value. The same holds for any other validated instrument (`otherInstrument`, E-057) that defines no total score.
- For the human: decide whether OUT-026 should read "total score, where the instrument defines one".

### ISS-08 Control levels under "responder or non-responder label"
- Stage 1: OUT-020 speaks of "a responder or non-responder label" and names the "IHS position statement 2025 control levels" as an example criterion. That criterion has four levels, not two.
- Evidence: [S-010] ISS-08/Q00.
- Effect on the model: the label category is either responder, non-responder or one of the four control levels (E-046); all other properties of OUT-020 apply to every category.
- For the human: confirm that control-level labels are responder labels in the sense of OUT-020.

### ISS-09 Which "acute medication outputs" OUT-029 breaks down by headache type
- Stage 1: OUT-029 (MUST) asks for "frequency and acute medication outputs separately for each headache type [...] as well as combined", without naming which acute-medication outputs it means. Group D of Stage 1 contains the acute-medication days of OUT-014 (total, by class and by drug), the weekly view of OUT-015 (SHOULD) and the medication-overuse indicator of OUT-016 (MUST).
- Evidence: [S-001] ISS-09/Q00.
- Effect on the model: INV-118 (C1-13) presents the acute-medication days of OUT-014 (total, per class and per drug) for each headache type and combined. The weekly view (E-036, INV-118 (C1-11)) and the medication-overuse indicator (E-032, INV-044) are required for all headache types combined only; an indicator per headache type would not correspond to the ICHD-3 levels.
- For the human: decide whether "acute medication outputs" in OUT-029 also covers the weekly view of OUT-015 and the medication-overuse indicator of OUT-016.

### ISS-10 Evaluation time points for preventive treatments outside the populations of the guidance quoted in OUT-018
- Stage 1: OUT-018 (MUST) asks, "For each preventive treatment", for the comparison "at the evaluation time points named in current guidance, which differ by treatment type". Every guidance that Stage 1 cites for OUT-018 concerns preventive treatment of migraine, and four of them concern adults only (AAN/AHS 2026, SIGN 155, the EHF 2022 guideline and the Russian clinical recommendations for adults). NICE CG150 covers people aged 12 years and older, and its 1.3.28 and 1.3.29 concern treatments that it recommends for adults; the IHS 2024 recommendations, the NVN module and the Turkish protocol also address children (E-041). Stage 1 also covers preventive treatments of other headache types (OUT-009: "tension-type headache, cluster headache", in the view with markers for preventive treatments; OUT-031: [S-014] "optimum acute and preventative treatments are maintained") and of children and adolescents (OUT-036 (d): "present efficacy of treatment from diary data as recommended in paediatric guidance").
- Evidence: [S-015], [S-034] ISS-10/Q00.
- Effect on the model: every evaluation rule applies only within the population of its guidance (E-041 `inPopulation`): to a preventive treatment given for migraine, for a subject who was, on the start of the treatment, of the ages the guidance covers. A response comparison is still required for every preventive treatment whose start the context states (INV-055; R-MCF (1)), but no guidance time point is required for a preventive treatment given only for another headache type. For a treatment started in childhood or adolescence, only the time points of guidance that covers that age are required: the NVN module, IHS 2024 Q2, the Turkish protocol, the Russian clinical recommendations for children and, from the age of 12, NICE CG150 1.3.27. The rule list holds every time point that the guidance cited for OUT-018 names (since v07; the time point of the Turkish protocol section 7.3 since v14), and, for children and adolescents, the [S-034] time point above, because OUT-036 (d) asks for the efficacy of treatment "as recommended in paediatric guidance" and Stage 1 cites [S-034] there (E-041/D01, E-041/D02).
- For the human: decide whether OUT-018 should name evaluation time points for preventive treatments of tension-type headache, cluster headache and other headache types; and confirm that the time point of the paediatric guidance [S-034], which Stage 1 cites for OUT-036 (d) but not for OUT-018, belongs to the time points of OUT-018 (E-041, `ruleRuChildren`).

### ISS-11 The NICE CG150 1.3.48 review window for children under 12
- Stage 1: OUT-017 asks, "For patients withdrawing from overused medication", for "the review window 4 to 8 weeks after the start of withdrawal named in NICE CG150 recommendation 1.3.48", with no age condition.
- Evidence: [S-015] ISS-11/Q00.
- Effect on the model: the model follows Stage 1. The withdrawal follow-up view shows the 4–8-week review window for every subject who is withdrawing from overused medication (E-039 `reviewWindow`, INV-051), including a child under 12, for whom NICE CG150 names no review window.
- For the human: decide whether the review window of OUT-017 applies to children under 12, or which guidance names one for them.

### ISS-12 Cluster remission duration in ICHD-3
- Stage 1: OUT-031 (SHOULD) asks, for patients with cluster headache, for "cluster periods (bouts) and cluster remission periods with their start dates, end dates and durations, using the ICHD-3 definitions". Its Evidence quotes the first sentence of the definition of "Cluster remission period" in the ICHD-3 Definitions of terms and adds that "the next sentence of the definition, a duration criterion, is not quoted". Its Caveats say that "The output shows the start date, end date and duration of each attack-free period", but not the element of that definition on attacks that cannot be induced with alcohol or nitroglycerine.
- Evidence: ICHD-3 words the duration of a cluster remission in three ways. [S-001] ISS-12/Q01, [S-001] ISS-12/Q02, [S-001] ISS-12/Q03.
- Effect on the model: E-063 and INV-089 follow the Definitions of terms, whose definition Stage 1 quotes for OUT-031: a remission period that shows its start date lasts more than three months (`remissionMoreThanMonths`, table SD-FX; INV-089), and every fully conformant output shows that date (E-063 `start`, SHOULD). An attack-free period of three months or less is therefore not shown as a remission period that shows its start date: neither one that 3.1.2 calls a remission (lasting less than three months), nor one of exactly three months, which 3.1.1 criterion B admits (at least three months). The time between two bouts that a cluster view shows remains visible from the end date of the one and the start date of the next (E-062 `bouts`, INV-089). The model reads the attack-free periods of the OUT-031 Caveat as the remission periods whose definition the Caveat discusses (E-063/D01). Where there is no attack-free period of more than three months to show, for example for a subject whose cluster headache has been chronic since its onset, `remissions` (E-062, SHOULD) stays empty, a deviation from that SHOULD for a reason in particular circumstances (section 3.1), as for any subject who has had no remission. The model adds no other kind of attack-free period.
- For the human: decide which ICHD-3 usage "the ICHD-3 definitions" of OUT-031 means for the duration of a cluster remission period: the Definitions of terms (an attack-free period of more than three months), which the model follows, or also the wording of 3.1.1 criterion B (at least three months) and of 3.1.2 (remissions lasting less than three months). In particular, decide whether attack-free periods of less than three months in chronic cluster headache, and attack-free periods of exactly three months, should be shown as remission periods, and, if so, whether the output should distinguish them from remissions in the sense of the Definitions of terms.

### ISS-13 Residual burden next to a percentage change over a period shorter than a month
- Stage 1: OUT-019 asks: "Wherever the output shows a relative (percentage) change in migraine or headache days, it SHOULD show next to it the absolute number of migraine days and moderate/severe headache days per month that remain on treatment." OUT-009 asks for weekly values where weekly granularity is clinically relevant, and the model admits a change between any two periods (E-040).
- Evidence: Stage 1 wording only. No calendar month or 28-day period lies within a compared period of fewer than 28 days, so a number "per month" within it does not exist (fix 02, item 14).
- Effect on the model: the residual burden is asked for next to every percentage change in migraine or headache days whose compared period has at least 28 days (INV-060 with INV-061). It is not asked for next to a change over a shorter compared period, for example between two calendar weeks.
- For the human: decide whether OUT-019 applies to percentage changes over periods shorter than a month, and if so, which month the residual burden then refers to (for example the calendar month or 28-day period that ends on the last day of the compared period).

ISS-07 was withdrawn in iteration 01 (section 9).

No output was found in the Stage 2 research that EBM supports and Stage 1 lacks. No Stage 1 source was found to be outdated by a newer version during the Stage 2 research.

## 9. Withdrawn and merged items

No element (E-NNN) has been withdrawn. The invariants below were merged in v35 into the item or items named in the last column (PROCESS.md sections 6a and 7); their IDs are not reused. One Stage 1 issue of section 8 has been withdrawn and is listed so that its ID is not reused.

| ID | Name | Iteration | Reason | Went into |
|---|---|---|---|---|
| INV-005 | A number of days does not exceed the period length | 35 | restructuring (PROCESS.md section 6a), merged | INV-121 |
| INV-007 | An annotation is shown with what it qualifies | 35 | restructuring (PROCESS.md section 6a), merged | E-010 `qualifies` (W2) |
| INV-009 | Headache days follow ICHD-3 | 35 | restructuring (PROCESS.md section 6a), merged | INV-125 (SD-DF-01) |
| INV-010 | Attacks follow ICHD-3 | 35 | restructuring (PROCESS.md section 6a), merged | INV-125 (SD-DF-02) |
| INV-013 | No completeness cut-off presented as clinically validated | 35 | restructuring (PROCESS.md section 6a), merged | INV-119 (C2-02) |
| INV-014 | Headache days per reporting period | 35 | restructuring (PROCESS.md section 6a), merged | INV-118 (C1-01) |
| INV-015 | Migraine days per reporting period, for patients with migraine | 35 | restructuring (PROCESS.md section 6a), merged | INV-118 (C1-02) |
| INV-016 | Moderate/severe headache days per reporting period | 35 | restructuring (PROCESS.md section 6a), merged | INV-118 (C1-03) |
| INV-017 | Attacks per reporting period | 35 | restructuring (PROCESS.md section 6a), merged | INV-118 (C1-05) |
| INV-108 | Moderate/severe headache days and attacks per calendar month or 28-day period, where provided | 35 | restructuring (PROCESS.md section 6a), merged | INV-118 (C1-04, C1-06) |
| INV-018 | Intensity summary per reporting period | 35 | restructuring (PROCESS.md section 6a), merged | INV-118 (C1-07) |
| INV-019 | Duration summary per reporting period | 35 | restructuring (PROCESS.md section 6a), merged | INV-118 (C1-08) |
| INV-020 | Durations of treated attacks are labelled as influenced by acute treatment | 35 | restructuring (PROCESS.md section 6a), merged | INV-120 (C3-03) |
| INV-021 | Durations of treated attacks are not a stand-alone efficacy measure | 35 | restructuring (PROCESS.md section 6a), merged | INV-119 (C2-03) |
| INV-022 | Associated symptoms and most bothersome symptom across periods, for migraine | 35 | restructuring (PROCESS.md section 6a), merged | INV-118 (C1-09) |
| INV-023 | Acute-medication days per reporting period: total, by class and by drug | 35 | restructuring (PROCESS.md section 6a), merged | INV-118 (C1-10) |
| INV-025 | Weekly view of acute-medication days | 35 | restructuring (PROCESS.md section 6a), merged | INV-118 (C1-11) |
| INV-026 | Functional impact per reporting period | 35 | restructuring (PROCESS.md section 6a), merged | INV-118 (C1-12) |
| INV-028 | Separate presentation per headache type | 35 | restructuring (PROCESS.md section 6a), merged | INV-118 (C1-13) |
| INV-029 | Intensity per headache type, where provided | 35 | restructuring (PROCESS.md section 6a), merged | INV-118 (C1-14) |
| INV-030 | Values per headache type do not exceed the combined values | 35 | restructuring (PROCESS.md section 6a), merged | INV-122 |
| INV-036 | Markers show the treatment course | 35 | restructuring (PROCESS.md section 6a), merged | INV-123; E-034 `event` (attribute type) |
| INV-043 | Three-month view assigns no diagnosis | 35 | restructuring (PROCESS.md section 6a), merged | INV-119 (C2-08) |
| INV-047 | Indicator worded as a prompt for clinical review | 35 | restructuring (PROCESS.md section 6a), merged | INV-120 (C3-04) |
| INV-048 | Indicator is not a diagnosis of medication-overuse headache | 35 | restructuring (PROCESS.md section 6a), merged | INV-119 (C2-04) |
| INV-113 | A withdrawal follow-up view shows a start of withdrawal of the subject | 35 | restructuring (PROCESS.md section 6a), merged | INV-123 |
| INV-052 | Label of the expected transient worsening | 35 | restructuring (PROCESS.md section 6a), merged | INV-120 (C3-06) |
| INV-054 | A change of a response comparison is shown with the values it compares | 35 | restructuring (PROCESS.md section 6a), merged | E-040 `reference`, `compared` (W2) |
| INV-117 | A responder label concerns one of the subject's preventive treatments | 35 | restructuring (PROCESS.md section 6a), merged | INV-123 |
| INV-065 | A responder label is not the sole indicator of individual benefit | 35 | restructuring (PROCESS.md section 6a), merged | INV-119 (C2-06) |
| INV-084 | Screening results are not psychiatric diagnoses | 35 | restructuring (PROCESS.md section 6a), merged | INV-119 (C2-09) |
| INV-090 | Caveats of the trigger co-occurrence view | 35 | restructuring (PROCESS.md section 6a), merged | INV-120 (C3-09) |
| INV-098 | Paediatric outputs are presented as supportive information | 35 | restructuring (PROCESS.md section 6a), merged | INV-120 (C3-11) |
| INV-099 | Interpretive caveats on every summary | 35 | restructuring (PROCESS.md section 6a), merged | INV-120 (C3-01) |
| INV-100 | Indicators, labels and associations require clinical interpretation | 35 | restructuring (PROCESS.md section 6a), merged | INV-120 (C3-05, C3-07, C3-08, C3-09, C3-10) |
| INV-101 | No output presented as replacing clinical assessment or as a diagnosis | 35 | restructuring (PROCESS.md section 6a), merged | INV-119 (C2-01) |
| INV-106 | No output decides on the continuation of a preventive treatment | 35 | restructuring (PROCESS.md section 6a), merged | INV-119 (C2-05) |
| INV-107 | No output decides which definition of acute treatment response applies | 35 | restructuring (PROCESS.md section 6a), merged | INV-119 (C2-07) |
| ISS-07 | Overlapping bands in two Stage 1 sources (a Stage 1 issue of section 8) | 01 | Not a gap or defect of Stage 1, which does not state the bands (review remark R01-12). The overlaps of the HALT-90 bands at 20 and of the IHS Q6 MIDAS baseline ranges at 20 remain described in E-057/D02 and E-045/D03. | — |

## 10. Sources

New Stage 2 sources only; Stage 1 sources S-001 to S-046 are cited by their Stage 1 IDs. Access date for every URL below: 2026-10-21. For PubMed Central articles, the same full text can be read in machine-readable form at `https://www.ebi.ac.uk/europepmc/webservices/rest/<PMCID>/fullTextXML`, which is where the quotes were checked.

| ID | Citation | Type and grading | Language | Year | DOI / PMID | URL where quotes can be verified |
|---|---|---|---|---|---|---|
| S-101 | Yang M, Rendas-Baum R, Varon SF, Kosinski M. Validation of the Headache Impact Test (HIT-6™) across episodic and chronic migraine. Cephalalgia 2011;31(3):357–367. | Primary study (validation study), co-authored by M. Kosinski, a developer of HIT-6 (QualityMetric); no grading | English | 2011 | 10.1177/0333102410379890 / PMID 20819842 / PMC3057423 | https://pmc.ncbi.nlm.nih.gov/articles/PMC3057423/ |
| S-102 | Pavlovic JM, Stewart WF, Bruce CA, Gorman JA, Sun H, Buse DC, Lipton RB. Burden of migraine related to menses: results from the AMPP study. J Headache Pain 2015;16:24. | Primary study (population-based study), co-authored by W.F. Stewart and R.B. Lipton, the developers of MIDAS; no grading | English | 2015 | 10.1186/s10194-015-0503-y / PMID 25902814 / PMC4406925 | https://pmc.ncbi.nlm.nih.gov/articles/PMC4406925/ |
| S-103 | Cincinnati Children's Hospital Medical Center, Headache Center. "PedMIDAS Tool for Assessing Migraine Disability" (web page "PedMIDAS Tool"). PedMIDAS was developed at this centre (Hershey AD, Powers SW, Vockell AL, et al. PedMIDAS: development of a questionnaire to assess disability of migraines in children. Neurology 2001;57(11):2034–2039, PMID 11739822). | Instrument documentation by the developers' institution; no grading | English | current page (page footer © 2026) | — (developer paper: 10.1212/wnl.57.11.2034 / PMID 11739822) | https://www.cincinnatichildrens.org/service/h/headache-center/pedmidas |
| S-104 | Snaith RP. The Hospital Anxiety And Depression Scale. Health Qual Life Outcomes 2003;1:29. | Commentary by a co-developer of the instrument; no grading | English | 2003 | 10.1186/1477-7525-1-29 / PMID 12914662 / PMC183845 | https://pmc.ncbi.nlm.nih.gov/articles/PMC183845/ |
| S-105 | Instruction manual: Instructions for Patient Health Questionnaire (PHQ) and GAD-7 Measures. The PHQ family of measures and the GAD-7 "were developed by Drs. Robert L. Spitzer, Janet B.W. Williams, Kurt Kroenke and colleagues, with an educational grant from Pfizer Inc." (manual, P. 8/9, section "Questions regarding development, acknowledgments and use"). Undated; PDF created 2010, modified 2014 (document metadata, author Kurt Kroenke). Copy hosted by The Joint Commission. | Instrument documentation by the developers; no grading | English | 2010 (PDF metadata) | — | https://manual.jointcommission.org/pub/BHCInstruments/RomInstr00054/instructions_PHQ.pdf |
| S-106 | National Institute for Health and Care Excellence. Botulinum toxin type A for the prevention of headaches in adults with chronic migraine. Technology appraisal guidance TA260. Published 27 June 2012; last reviewed 11 January 2016. NICE CG150 [S-015] recommendation 1.3.26 refers to it "For full details". | Health technology appraisal guidance of a national body (NICE technology appraisal; recommendations on clinical and cost-effectiveness; no evidence grading) | English | 2012 | — | https://www.nice.org.uk/guidance/ta260/chapter/2-The-technology |

## 11. Source data tables

Each table of this section is a case table (section 2.11). Its formal cells are the values that a source, or Stage 1, fixes and that the outputs show or relate; the informative columns name the source and the `RATIONALE.md` entries that hold the verbatim quotes. Rows are identified by `SD-<table>-NN` (section 4.2).

### 11.1 SD-IC ICHD-3 code labels

Case table SD-IC — form C: cases of the given function `label` (E-009)

| Row | `k : ICHD3Code` | `label(k)` | Source | Rationale |
|---|---|---|---|---|
| SD-IC-01 | `c1` | `"1. Migraine"` | [S-001] | E-009/Q01 |
| SD-IC-02 | `c1_2` | `"1.2 Migraine with aura"` | [S-001] | E-009/Q01 |
| SD-IC-03 | `c1_3` | `"1.3 Chronic migraine"` | [S-001] | E-009/Q01 |
| SD-IC-04 | `c2` | `"2. Tension-type headache (TTH)"` | [S-001] | E-009/Q01 |
| SD-IC-05 | `c2_3` | `"2.3 Chronic tension-type headache"` | [S-001] | E-009/Q01 |
| SD-IC-06 | `c3_1` | `"3.1 Cluster headache"` | [S-001] | E-009/Q02 |
| SD-IC-07 | `c8_2` | `"8.2 Medication-overuse headache (MOH)"` | [S-001] | E-009/Q03 |
| SD-IC-08 | `c8_2_1` | `"8.2.1 Ergotamine-overuse headache"` | [S-001] | E-009/Q03 |
| SD-IC-09 | `c8_2_2` | `"8.2.2 Triptan-overuse headache"` | [S-001] | E-009/Q03 |
| SD-IC-10 | `c8_2_3` | `"8.2.3 Non-opioid analgesic-overuse headache"` | [S-001] | E-009/Q03 |
| SD-IC-11 | `c8_2_4` | `"8.2.4 Opioid-overuse headache"` | [S-001] | E-009/Q03 |
| SD-IC-12 | `c8_2_5` | `"8.2.5 Combination-analgesic-overuse headache"` | [S-001] | E-009/Q03 |
| SD-IC-13 | `c8_2_6` | `"8.2.6 Medication-overuse headache attributed to multiple drug classes not individually overused"` | [S-001] | E-009/Q03 |
| SD-IC-14 | `c8_2_7` | `"8.2.7 Medication-overuse headache attributed to unspecified or unverified overuse of multiple drug classes"` | [S-001] | E-009/Q03 |
| SD-IC-15 | `c8_2_8` | `"8.2.8 Medication-overuse headache attributed to other medication"` | [S-001] | E-009/Q03 |

### 11.2 SD-DF Definitions that Stage 1 fixes

Case table SD-DF — form C: cases of the given partial functions `fixedDefinition` and `fixedDefinitionLevel` (E-011), read by INV-125

| Row | `k : LabelledMeasure` | `fixedDefinition(k)` | `fixedDefinitionLevel(k)` | Stage 1 part |
|---|---|---|---|---|
| SD-DF-01 | `headacheDaysMeasure` | `ichd3HeadacheDays` | `must` | Stage 1 OUT-004 (MUST: "with 'headache days' as defined in ICHD-3 'Definitions of terms'") |
| SD-DF-02 | `attacksMeasure` | `ichd3FrequencyOfAttacks` | `should` | Stage 1 OUT-007 (SHOULD) |

### 11.3 SD-CLS Acute drug classes of ICHD-3 8.2

Case table SD-CLS — form C: cases of the given functions `classCode` (E-028) and `overuseLevel` (E-032) for each class

| Row | `k : AcuteDrugClass` | `classCode(k)` | `overuseLevel(ofClassUse(k))` | Source | Rationale |
|---|---|---|---|---|---|
| SD-CLS-01 | `ergotamine` | `c8_2_1` | `10` | [S-001] | E-009/Q03; E-032/Q01, Q02 |
| SD-CLS-02 | `triptans` | `c8_2_2` | `10` | [S-001] | E-009/Q03; E-032/Q01, Q03 |
| SD-CLS-03 | `nonOpioidAnalgesics` | `c8_2_3` | `15` | [S-001] | E-009/Q03; E-032/Q01, Q04 |
| SD-CLS-04 | `opioids` | `c8_2_4` | `10` | [S-001] | E-009/Q03; E-032/Q01, Q05 |
| SD-CLS-05 | `combinationAnalgesics` | `c8_2_5` | `10` | [S-001] | E-009/Q03; E-032/Q01, Q06 |
| SD-CLS-06 | `otherMedication` | `c8_2_8` | `10` | [S-001] | E-009/Q03; E-032/Q01, Q07 |

### 11.4 SD-CMB Combined use (ICHD-3 8.2.6)

Case table SD-CMB — form C: cases of the given functions `overuseCode`, `overuseLevel` and `basisScope` (E-032) for combined use

| Row | `k : OveruseScope` | `overuseCode(k)` | `overuseLevel(k)` | `basisScope(k)` | Source | Rationale |
|---|---|---|---|---|---|---|
| SD-CMB-01 | `combinedUse` | `c8_2_6` | `10` | `ofClasses(classesOf826)` | [S-001] | E-028/Q02, E-028/Q03; E-032/Q01 |

### 11.5 SD-FX Fixed numbers

Case table SD-FX — form D: defined constants

| Row | `k` | `type` | `value` | Unit or gloss | Used in | Source | Rationale |
|---|---|---|---|---|---|---|---|
| SD-FX-01 | `windowDaysBefore` | `ℕ` | `2` | day −2 is 2 days before day 1 | E-060 | [S-001] | E-060/Q01, E-060/Q02 |
| SD-FX-02 | `windowDaysAfter` | `ℕ` | `2` | day +3 is 2 days after day 1, because there is no day 0 | E-060 | [S-001] | E-060/Q01, E-060/Q02 |
| SD-FX-03 | `reviewWindowFromWeeks` | `ℕ₁` | `4` | weeks | E-039 | [S-015] | Stage 1 OUT-017 (statement) |
| SD-FX-04 | `reviewWindowToWeeks` | `ℕ₁` | `8` | weeks | E-039 | [S-015] | Stage 1 OUT-017 (statement) |
| SD-FX-05 | `followUpMonths` | `ℕ₁` | `12` | "over the following year"; months | E-039 | [S-015] | Stage 1 OUT-017 (statement) |
| SD-FX-06 | `overuseSpanMonths` | `ℕ₁` | `3` | the time span is more than 3 months | E-032 | [S-001] | E-032/Q01–Q07 |
| SD-FX-07 | `remissionMoreThanMonths` | `ℕ₁` | `3` | months | E-063 | [S-001] | E-063/Q01 |
| SD-FX-08 | `shortestMonthlyDays` | `ℕ₁` | `28` | the length of a 28-day period; no calendar month is shorter; unit: days | E-042 | — | Stage 1 OUT-001 (statement) |

### 11.6 SD-ER Evaluation rules of current guidance

Case table SD-ER — form V: constants of the value type `EvaluationRule` (E-041), collected in `evaluationRules`

| Row | `k` | `guidance` | `headacheType` | `ages` | `appliesTo` | `excludes` | `anchor` | `timing` | `minOffset` | `maxOffset` | Rationale |
|---|---|---|---|---|---|---|---|---|---|---|---|
| SD-ER-01 | `ruleNice1327` | `"NICE CG150 rec. 1.3.27"` | `c1` | `aged12AndOver` | `allPreventiveTypes` | `∅` | `treatmentStartAnchor` | `withinWindow` | `months(3)` | `{months(6)}` | E-041/Q00, Q01, Q02, Q29, Q30 |
| SD-ER-02 | `ruleNice1328` | `"NICE CG150 rec. 1.3.28"` | `c1` | `adultsOnly` | `{cgrpInhibitor}` | `∅` | `treatmentStartAnchor` | `atOffset` | `weeks(12)` | `∅` | E-041/Q00, Q01, Q02, Q03 |
| SD-ER-03 | `ruleNice1329` | `"NICE CG150 rec. 1.3.29"` | `c1` | `adultsOnly` | `{onabotulinumtoxinA}` | `∅` | `endOfCycleAnchor(2)` | `atOffset` | `weeks(0)` | `∅` | E-041/Q00, Q01, Q02, Q04 |
| SD-ER-04 | `ruleAan14A` | `"AAN/AHS 2026 rec. 14A"` | `c1` | `adultsOnly` | `allPreventiveTypes` | `{onabotulinumtoxinA}` | `toleratedOrTargetDoseAnchor` | `withinWindow` | `weeks(8)` | `{weeks(12)}` | E-041/Q00, Q05, Q07 |
| SD-ER-05 | `ruleAan14B` | `"AAN/AHS 2026 rec. 14B"` | `c1` | `adultsOnly` | `{onabotulinumtoxinA}` | `∅` | `toleratedOrTargetDoseAnchor` | `atLeastOffset` | `weeks(24)` | `∅` | E-041/Q00, Q05, Q06 |
| SD-ER-06 | `ruleSignTitrated` | `"SIGN 155 section 4.1 (titrated treatment)"` | `c1` | `adultsOnly` | `{doseTitratedPreventive}` | `∅` | `toleratedOrTargetDoseAnchor` | `atLeastOffset` | `weeks(8)` | `∅` | E-041/Q00, Q08, Q09 |
| SD-ER-07 | `ruleSignFixedDose` | `"SIGN 155 section 4.1 (fixed-dose treatment)"` | `c1` | `adultsOnly` | `{fixedDosePreventive}` | `∅` | `treatmentStartAnchor` | `atOffset` | `months(3)` | `∅` | E-041/Q00, Q08, Q09 |
| SD-ER-08 | `ruleEhf2022Q3` | `"EHF 2022 guideline, expert consensus statement, question 3"` | `c1` | `adultsOnly` | `{antiCGRPMonoclonalAntibody}` | `∅` | `treatmentStartAnchor` | `atLeastOffset` | `months(3)` | `∅` | E-041/Q00, Q10, Q11 |
| SD-ER-09 | `ruleIhsQ2Oral` | `"IHS global practice recommendations Q2 (oral preventives)"` | `c1` | `anyAge` | `{oralPreventive}` | `∅` | `toleratedOrTargetDoseAnchor` | `atOffset` | `months(3)` | `∅` | E-041/Q00, Q12, Q13, Q14 |
| SD-ER-10 | `ruleIhsQ2Monthly` | `"IHS global practice recommendations Q2 (monthly injectables)"` | `c1` | `anyAge` | `{monthlyInjectable}` | `∅` | `treatmentStartAnchor` | `atLeastOffset` | `months(3)` | `∅` | E-041/Q00, Q14 |
| SD-ER-11 | `ruleIhsQ2Quarterly` | `"IHS global practice recommendations Q2 (quarterly injectables)"` | `c1` | `anyAge` | `{quarterlyInjectable}` | `∅` | `treatmentStartAnchor` | `atLeastOffset` | `months(6)` | `∅` | E-041/Q00, Q14 |
| SD-ER-12 | `ruleNvnTitrated` | `"NVN guideline Hoofdpijn, module Profylactische behandeling migraine (titrated prophylactics)"` | `c1` | `anyAge` | `{doseTitratedPreventive}` | `∅` | `treatmentStartAnchor` | `withinWindow` | `months(2)` | `{months(3)}` | E-041/Q00, Q15 |
| SD-ER-13 | `ruleRu71` | `"Russian clinical recommendations «Мигрень» (adults) 2024, section 7.1"` | `c1` | `adultsOnly` | `allPreventiveTypes` | `{onabotulinumtoxinA}` | `treatmentStartAnchor` | `atOffset` | `months(3)` | `∅` | E-041/Q00, Q16, Q17 |
| SD-ER-14 | `ruleRu33Bta` | `"Russian clinical recommendations «Мигрень» (adults) 2024, section 3.3 (botulinum toxin type A)"` | `c1` | `adultsOnly` | `{onabotulinumtoxinA}` | `∅` | `treatmentStartAnchor` | `atLeastOffset` | `months(6)` | `∅` | E-041/Q00, Q16, Q17, Q18 |
| SD-ER-15 | `ruleRuChildren` | `"Russian clinical recommendations «Мигрень» (children) 2024, appendix Б (flowchart)"` | `c1` | `childrenAndAdolescentsOnly` | `allPreventiveTypes` | `∅` | `treatmentStartAnchor` | `atOffset` | `months(3)` | `∅` | E-041/Q00, Q19, Q20, Q21 |
| SD-ER-16 | `ruleTrBox8` | `"Turkish Ministry of Health Migraine Clinical Protocol 2025, section 3.6.2, Box 8"` | `c1` | `anyAge` | `allPreventiveTypes` | `{onabotulinumtoxinA}` | `treatmentStartAnchor` | `withinWindow` | `months(2)` | `{months(3)}` | E-041/Q00, Q22, Q24, Q25, Q27 |
| SD-ER-17 | `ruleTr3639` | `"Turkish Ministry of Health Migraine Clinical Protocol 2025, section 3.6.3.9 (onabotulinumtoxinA)"` | `c1` | `anyAge` | `{onabotulinumtoxinA}` | `∅` | `endOfCycleAnchor(3)` | `atOffset` | `weeks(0)` | `∅` | E-041/Q00, Q23, Q24 |
| SD-ER-18 | `ruleTr73` | `"Turkish Ministry of Health Migraine Clinical Protocol 2025, section 7.3 (botulinum toxin injection)"` | `c1` | `anyAge` | `{onabotulinumtoxinA}` | `∅` | `endOfCycleAnchor(2)` | `atLeastOffset` | `weeks(0)` | `∅` | E-041/Q00, Q24, Q26, Q27, Q28 |

### 11.7 SD-RC Named responder criteria

Case table SD-RC — form V: constants of the value type `ResponderCriterion` (E-045), collected in `namedCriteria`

| Row | `k` | `name` | `components` | `alsoRestsOn` | Rationale |
|---|---|---|---|---|---|
| SD-RC-01 | `critNice1328` | `"NICE CG150 rec. 1.3.28"` | `{reductionFromBaseline(ReductionComponent(measures ↦ {migraineDays}, atLeastPercent ↦ 50, condition ↦ episodicMigraineOnly)),<br>reductionFromBaseline(ReductionComponent(measures ↦ {migraineDays}, atLeastPercent ↦ 30, condition ↦ chronicMigraineOnly))}` | `∅` | E-045/Q00 |
| SD-RC-02 | `critNice1329` | `"NICE CG150 rec. 1.3.29"` | `{reductionFromBaseline(ReductionComponent(measures ↦ {headacheDays}, atLeastPercent ↦ 30, condition ↦ anySubject))}` | `∅` | E-045/Q00 |
| SD-RC-03 | `critIhsQ6` | `"IHS global practice recommendations Q6"` | `{reductionFromBaseline(ReductionComponent(measures ↦ {migraineDays, moderateSevereHeadacheDays}, atLeastPercent ↦ 50, condition ↦ anySubject)),<br>reductionFromBaseline(ReductionComponent(measures ↦ {migraineDays, moderateSevereHeadacheDays}, atLeastPercent ↦ 30, condition ↦ ihsQ6ChronicAlternativeOnly)),<br>judgement("a clinically meaningful subjective improvement as reported by the person with migraine or evaluated by Patient Global Impression scales"),<br>scoreDecrease(ScoreComponent(instrument ↦ midas, decrease ↦ atLeastPoints(5), baselineAtLeast ↦ {11}, baselineAtMost ↦ {20}, condition ↦ anySubject)),<br>scoreDecrease(ScoreComponent(instrument ↦ midas, decrease ↦ atLeastPercentOfBaseline(30), baselineAtLeast ↦ {20}, baselineAtMost ↦ ∅, condition ↦ anySubject)),<br>scoreDecrease(ScoreComponent(instrument ↦ hit6, decrease ↦ atLeastPoints(5), baselineAtLeast ↦ ∅, baselineAtMost ↦ ∅, condition ↦ anySubject))}` | `{instrumentResultOf(pgic), instrumentResultOf(midas), instrumentResultOf(hit6)}` | E-045/Q00, Q01, Q02 |
| SD-RC-04 | `critIhs2025` | `"IHS position statement 2025 control levels"` | `{controlLevels}` | `{acuteTreatmentEffectiveness}` | E-045/Q00; E-046/Q01–Q05 |
| SD-RC-05 | `critDmkg` | `"DMKG/ÖKSG/SKG consensus statement (episodic migraine)"` | `{reductionFromBaseline(ReductionComponent(measures ↦ {migraineDays}, atLeastPercent ↦ 50, condition ↦ episodicMigraineOnly)),<br>scoreDecrease(ScoreComponent(instrument ↦ hit6, decrease ↦ atLeastPoints(5), baselineAtLeast ↦ ∅, baselineAtMost ↦ ∅, condition ↦ episodicMigraineOnly)),<br>scoreDecrease(ScoreComponent(instrument ↦ midas, decrease ↦ atLeastPercentOfBaseline(30), baselineAtLeast ↦ ∅, baselineAtMost ↦ ∅, condition ↦ episodicMigraineOnly))}` | `{instrumentResultOf(hit6), instrumentResultOf(midas)}` | E-045/Q00 |
| SD-RC-06 | `critRu71` | `"Russian clinical recommendations «Мигрень» (adults) 2024, section 7.1"` | `{reductionFromBaseline(ReductionComponent(measures ↦ {headacheDays}, atLeastPercent ↦ 50, condition ↦ anySubject))}` | `∅` | E-045/Q00 |

### 11.8 SD-CL Control levels of the IHS position statement 2025

Case table SD-CL — form C: definition by cases of `inControlRange`, `controlMinMonths` and `forcedAbove` (E-046), read by INV-064

| Row | `k : ControlLevel` | `inControlRange(k, n)` | `controlMinMonths(k)` | `forcedAbove(k)` | Source | Rationale |
|---|---|---|---|---|---|---|
| SD-CL-01 | `migraineFreedom` | `n = 0` | — | — | [S-010] | E-046/Q01 |
| SD-CL-02 | `optimalControl` | `n < 4` | `{3}` | — | [S-010] | E-046/Q02 |
| SD-CL-03 | `modestControl` | `4 ≤ n ∧ n ≤ 6` | — | — | [S-010] | E-046/Q03 |
| SD-CL-04 | `insufficientControl` | `true` | — | `{6}` | [S-010] | E-046/Q04, Q05 |

### 11.9 SD-IN Instruments

Case table SD-IN — form C: cases of the given functions `instrumentName`, `publishedRecall` (partial), `scoreRange` (partial) and `publishedGrading` (E-057)

| Row | `k : Instrument` | `instrumentName(k)` | `publishedRecall(k)` | `scoreRange(k)` | `publishedGrading(k)` | Rationale |
|---|---|---|---|---|---|---|
| SD-IN-01 | `midas` | `"MIDAS"` | `recallMonths(3)` | `ScoreRange(low ↦ 0, high ↦ ∅)` | `true` | E-057/Q03, Q04, Q10 |
| SD-IN-02 | `hit6` | `"HIT-6"` | `recallMonths(1)` | `ScoreRange(low ↦ 36, high ↦ {78})` | `true` | E-057/Q00, Q01, Q02, Q10 |
| SD-IN-03 | `msq21` | `"MSQ v2.1"` | — | — | — | Stage 1 OUT-026 (names) |
| SD-IN-04 | `halt90` | `"HALT-90"` | `recallMonths(3)` | `ScoreRange(low ↦ 0, high ↦ ∅)` | `true` | E-057/Q06, Q08, Q09, Q10 |
| SD-IN-05 | `halt30` | `"HALT-30"` | `recallMonths(1)` | `ScoreRange(low ↦ 0, high ↦ ∅)` | `false` | E-057/Q00, Q07, Q08, Q10 |
| SD-IN-06 | `hurt` | `"HURT"` | — | — | `true` | E-057/Q00 |
| SD-IN-07 | `mtoq` | `"M-TOQ"` | — | — | — | Stage 1 OUT-026 (names) |
| SD-IN-08 | `pedmidas` | `"PedMIDAS"` | `recallMonths(3)` | `ScoreRange(low ↦ 0, high ↦ ∅)` | `true` | E-057/Q00, Q05, Q10 |
| SD-IN-09 | `pgic` | `"PGIC"` | — | — | — | Stage 1 OUT-026 (names) |

### 11.10 SD-GB Grade bands

Case table SD-GB — form M: members of `const gradeBands : set1 GradeBand` (E-057)

| Row | `instrument` | `grade` | `label` | `low` | `strictLow` | `high` | Rationale |
|---|---|---|---|---|---|---|---|
| SD-GB-01 | `midas` | `{"I"}` | `"little or no disability"` | `0` | `false` | `{5}` | E-057/Q03 |
| SD-GB-02 | `midas` | `{"II"}` | `"mild disability"` | `6` | `false` | `{10}` | E-057/Q03 |
| SD-GB-03 | `midas` | `{"III"}` | `"moderate disability"` | `11` | `false` | `{20}` | E-057/Q03 |
| SD-GB-04 | `midas` | `{"IV"}` | `"severe disability"` | `21` | `false` | `∅` | E-057/Q03 |
| SD-GB-05 | `hit6` | `∅` | `"little or no impact"` | `36` | `false` | `{49}` | E-057/Q02 |
| SD-GB-06 | `hit6` | `∅` | `"some impact"` | `50` | `false` | `{55}` | E-057/Q02 |
| SD-GB-07 | `hit6` | `∅` | `"substantial impact"` | `56` | `false` | `{59}` | E-057/Q02 |
| SD-GB-08 | `hit6` | `∅` | `"severe impact"` | `60` | `false` | `{78}` | E-057/Q02 |
| SD-GB-09 | `pedmidas` | `∅` | `"Little to none"` | `0` | `false` | `{10}` | E-057/Q05 |
| SD-GB-10 | `pedmidas` | `∅` | `"Mild"` | `11` | `false` | `{30}` | E-057/Q05 |
| SD-GB-11 | `pedmidas` | `∅` | `"Moderate"` | `31` | `false` | `{50}` | E-057/Q05 |
| SD-GB-12 | `pedmidas` | `∅` | `"Severe"` | `50` | `true` | `∅` | E-057/Q05 |
| SD-GB-13 | `halt90` | `{"I"}` | `"Minimal or infrequent"` | `0` | `false` | `{5}` | E-057/Q09 |
| SD-GB-14 | `halt90` | `{"II"}` | `"Mild or infrequent"` | `6` | `false` | `{10}` | E-057/Q09 |
| SD-GB-15 | `halt90` | `{"III"}` | `"Moderate"` | `11` | `false` | `{20}` | E-057/Q09 |
| SD-GB-16 | `halt90` | `{"IV"}` | `"Severe"` | `20` | `false` | `∅` | E-057/Q09 |

### 11.11 SD-SC Screening instrument names

Case table SD-SC — form C: cases of the given function `screeningName` (E-059)

| Row | `k : ScreeningInstrument` | `screeningName(k)` | Rationale |
|---|---|---|---|
| SD-SC-01 | `hads` | `"HADS"` | Stage 1 OUT-033 (names) |
| SD-SC-02 | `phq9` | `"PHQ-9"` | Stage 1 OUT-033 (names) |
| SD-SC-03 | `gad7` | `"GAD-7"` | Stage 1 OUT-033 (names) |

### 11.12 SD-SR Screening score ranges

Case table SD-SR — form C: cases of the given partial function `screeningMax` (E-059), read by INV-085

| Row | `i : ScreeningInstrument` | `s : Subscale` | `screeningMax(i, s)` | Source | Rationale |
|---|---|---|---|---|---|
| SD-SR-01 | `hads` | `anxietySubscale` | `21` | [S-104] | E-059/Q01 |
| SD-SR-02 | `hads` | `depressionSubscale` | `21` | [S-104] | E-059/Q01 |
| SD-SR-03 | `phq9` | `wholeScale` | `27` | [S-105] | E-059/Q02 |
| SD-SR-04 | `gad7` | `wholeScale` | `21` | [S-105] | E-059/Q03 |

### 11.13 SD-ET Early time points of acute-treatment summaries

Case table SD-ET — form C: definition by cases of `earlyTimePointType` (E-050), read by INV-073

| Row | `k : EarlyTimePoint` | `earlyTimePointType(k)` | Stage 1 part |
|---|---|---|---|
| SD-ET-01 | `fifteenMinutes` | `{c3_1}` | Stage 1 OUT-023 ("For cluster headache, the corresponding time point is 15 minutes"), OUT-031 |
| SD-ET-02 | `twoHours` | `∅` | Stage 1 OUT-023 (the time point of every other summary) |

## 12. Change log

One entry per version. The details of v00 to v34 are in `history/vNN.md` and `fixes/fix-iter-NN.md`.

- v00 (iteration 00, 2026-10-21): Initial draft by the author. Notation OMN defined (section 2). 67 elements (E-001 to E-067) and 105 invariants (INV-001 to INV-105) realising all 39 Stage 1 requirements, each traced with full coverage (section 7). Thresholds, reference levels, offsets and score bands that are part of the output data are stated with verbatim quotes: ICHD-3 codes, the 8.2 reference levels and time span, the A1.1 perimenstrual window and the remission duration ([S-001]); the IHS Q6 thresholds ([S-008]) and IHS 2025 control levels ([S-010]); HALT recall, units and grading ([S-014]); HIT-6, MIDAS, PedMIDAS, HADS, PHQ-9 and GAD-7 value sets (new sources S-101 to S-105). Eight Stage 1 issues listed (ISS-01 to ISS-08). Mechanical checks run by script (IDs, references, declared names, attribute selections, traceability, conformance levels against Stage 1 statement strength).
- v01 (iteration 01, 2026-10-21): Fix of review iteration 01 (12 remarks; fixes/fix-iter-01.md).
- v02 (iteration 02, 2026-10-21): Fix of review iteration 02 (7 remarks; fixes/fix-iter-02.md), with a satisfiability pass over all MUST and SHOULD constraints.
- v03 (iteration 03, 2026-10-21): Fix of review iteration 03 (7 remarks; fixes/fix-iter-03.md), with a satisfiability pass over the changed invariants and attributes and over those that constrain the same elements and views.
- v04 (iteration 04, 2026-10-21): Fix of review iteration 04 (4 remarks; fixes/fix-iter-04.md), with a satisfiability pass over the changed invariants and attributes and over those that constrain the same elements and views.
- v05 (iteration 05, 2026-10-21): Fix of review iteration 05 (3 remarks; fixes/fix-iter-05.md), with a satisfiability pass over the changed invariants and attributes and over those that constrain the same elements and views.
- v06 (iteration 06, 2026-10-21): Fix of review iteration 06 (1 remark; fixes/fix-iter-06.md), with a satisfiability pass over the changed invariants and attributes and over those that constrain the same elements and views.
- v07 (iteration 07, 2026-10-21): Fix of review iteration 07 (3 remarks; fixes/fix-iter-07.md), with a completeness sweep of the evaluation time points of E-041 over the Stage 1 sources of OUT-018 and OUT-036 (d), and a satisfiability pass over the changed constructs and the invariants that use them.
- v08 (iteration 08, 2026-10-21): Fix of review iteration 08, re-check b (2 remarks; fixes/fix-iter-08.md; review 08 found no remarks), with a satisfiability pass over the changed constructs and the invariants that constrain the same elements and views.
- v09 (iteration 09, 2026-10-21): Fix of review iteration 09 (1 remark; fixes/fix-iter-09.md), with a satisfiability pass over the changed constructs and the invariants that constrain the same elements and views.
- v10 (iteration 10, 2026-10-21): Fix of review iteration 10, re-check b (2 remarks; fixes/fix-iter-10.md; review 10 found no remarks), with a whole-model sweep of conformance levels against the strength of the Stage 1 statement parts over the whole range each constraint covers, a whole-model sweep of the explanatory text against the formal text, and a satisfiability pass over the changed constructs and the invariants that constrain the same elements and views.
- v11 (iteration 11, 2026-10-21): Fix of review iteration 11 (3 remarks; fixes/fix-iter-11.md), with three whole-model sweeps (co-presence of the parts of an item in its view, quantifiers of presence requirements, and the range of context components) and a satisfiability pass over the changed constructs and the invariants that constrain the same elements and views.
- v12 (iteration 12, 2026-10-21): Fix of review iteration 12 (2 remarks; fixes/fix-iter-12.md), with two whole-model sweeps (the time frame of every context component; the triggers of every cross-cutting requirement) and a satisfiability pass over the changed constructs and the invariants that constrain the same elements and views.
- v13 (iteration 13, 2026-10-21): Fix of review iteration 13 (3 remarks; fixes/fix-iter-13.md), with a satisfiability pass over the changed constructs and the invariants that constrain the same elements and views; no whole-model sweep.
- v14 (iteration 14, 2026-10-21): Fix of review iteration 14 (2 remarks; fixes/fix-iter-14.md), with a satisfiability pass over the changed constructs and the invariants that constrain the same elements and views; no whole-model sweep.
- v15 (iteration 15, 2026-10-21): Fix of review iteration 15 (3 remarks; fixes/fix-iter-15.md), with an identifying-property check of every presence requirement (the scope, period or window, treatment or course, drug and formulation, instrument, age period and view of each required item) and a satisfiability pass over the changed constructs and the invariants that constrain the same elements and views; no other sweep.
- v16 (iteration 16, 2026-10-21): Fix of review iteration 16 (1 remark; fixes/fix-iter-16.md), with an identifying-property check of every item that INV-105 requires and a satisfiability pass over the changed constructs and the invariants that constrain the same elements and views; no other sweep.
- v17 (iteration 17, 2026-10-21): Fix of review iteration 17 (3 remarks; fixes/fix-iter-17.md), with a check of every comparison of a date with the first or last day of a period under the day convention stated in this version, and a satisfiability pass over the changed constructs and the invariants that constrain the same elements and views; no other sweep.
- v18 (iteration 18, 2026-10-21): Fix of review iteration 18 (1 remark; fixes/fix-iter-18.md), with a check of the other places where the model speaks of a treatment's on-treatment periods, and a satisfiability pass over the changed constructs and the invariants that constrain the same elements and views; no other sweep.
- v19 (iteration 19, 2026-10-21): Fix of re-check c of review iteration 19 (2 remarks; fixes/fix-iter-19.md). Review 19 and re-check 19b returned no remarks on v18. Both fixes are text only: no value, axiom, predicate, conformance level, Realises field or traceability row changed, and no `omn` block changed; no other sweep.
- v20 (iteration 20, 2026-10-21): Fix of review iteration 20 (1 remark; fixes/fix-iter-20.md). The fix is text only: no value, axiom, predicate, conformance level, Realises field or Elements or Invariants column of the traceability table changed, and no `omn` block changed. One check for the same defect: the ISS-03 list against every Stage 1 Statement that mentions migraine. No other sweep.
- v21 (iteration 21, 2026-10-21): Fix of re-check b of review iteration 21 (1 remark; fixes/fix-iter-21.md). Review 21 returned no remarks on v20. The fix is text only: no value, axiom, predicate, conformance level, Realises field or Elements or Invariants column of the traceability table changed, and no `omn` block changed. No other sweep.
- v22 (iteration 22, 2026-10-21): Fix of re-check b of review iteration 22 (1 remark; fixes/fix-iter-22.md). Review 22 returned no remarks on v21. One `omn` block changed: E-006, where `fillsPeriod` gains one conjunct. No value, axiom, conformance level, Realises field, or Elements or Invariants column of the traceability table changed. A satisfiability check by script covered every use of `fillsPeriod` (INV-050, INV-104, INV-105); no other sweep.
- v23 (iteration 23, 2026-10-21): Fix of review iteration 23 (1 remark; fixes/fix-iter-23.md). Two `omn` blocks changed: E-063 (the comment of `ongoing` and the definition of `lastDay`) and INV-089 (one conjunct added). No value, axiom, conformance level, Realises field, or Elements or Invariants column of the traceability table changed. One check for the same defect covered every item with an open end or a duration bound (cluster periods and remission periods, cycle lines, treatment lines, the withdrawal follow-up view, the post-stop monitoring view, treated-attack lines, adherence windows and the span of the medication-overuse indicator); no other instance was found, and nothing else was changed.
- v24 (iteration 24, 2026-10-21): Fix of review iteration 24 (2 remarks; fixes/fix-iter-24.md). Twelve `omn` blocks changed: E-014 (`daysOf`), E-032 (new `sameIndicatedPeriod`; `classShownUsed`, `classUseExcluded`), E-046 (`reductionMet`, `reductionDecided`, `attackReductionMet`, `attackReductionDecided`), INV-006, INV-012, INV-030, INV-031, INV-033, INV-046, INV-053, INV-089 and the new INV-111. No value, axiom, attribute declaration or conformance level of an existing item changed; one invariant was added.
- v25 (iteration 25, 2026-10-22): Fix of re-check b of review iteration 25 (1 remark; fixes/fix-iter-25.md). Review 25 returned no remarks on v24. One `omn` block changed: INV-001, which gains two conjuncts. No value, axiom, attribute declaration, defined predicate or function, or conformance level changed; INV-001 gains OUT-022 in its Realises field, and row OUT-022 gains INV-001.
- v26 (iteration 26, 2026-10-22): Fix of review iteration 26 (1 remark; fixes/fix-iter-26.md). Four `omn` blocks changed: E-008 (a new component `resumes` of `SubjectProfile`; new `resumesFrom` and `originalStart`), INV-001 (two conjuncts added), INV-070 (the baseline conjunct reads `originalStart` instead of `startOf`) and E-049 (the comment of `baseline` only). No value, axiom, conformance level, level-annotated attribute declaration, Realises field, or Elements or Invariants column of the traceability table changed.
- v27 (iteration 27, 2026-10-22): Fix of review iteration 27 (1 remark; fixes/fix-iter-27.md). Three `omn` blocks changed: E-008 (`originalStart` redefined), E-049 (the `baseline` attribute gains a `when` clause) and INV-070 (the baseline conjunct). No value, axiom, conformance level, Realises field, declared name, or Elements or Invariants column of the traceability table changed; INV-001 and every other predicate are byte-identical.
- v28 (iteration 28, 2026-10-22): Fix of review iteration 28 (2 remarks; fixes/fix-iter-28.md). Nine `omn` blocks changed: E-008 (a new predicate, `courseBegunBy`), INV-064, INV-067, INV-068, INV-070, INV-078, INV-079, INV-103 and INV-109. No value, axiom, conformance level, Realises field, level-annotated attribute declaration, or Elements or Invariants column of the traceability table changed. The E-049 `when` clauses, `originalStart`, INV-001, section 2.8 and every other watch-point-4 item are byte-identical.
- v29 (iteration 29, 2026-10-22): Fix of review iteration 29 (1 remark; fixes/fix-iter-29.md). The fix is text only: no `omn` block, value, axiom, conformance level, Realises field, level-annotated attribute declaration, or Elements or Invariants column of the traceability table changed. The INV-067 predicate, `courseBegunBy` and every formal block that the watch points of the oscillation check after iteration 28 name are byte-identical.
- v30 (iteration 30, 2026-10-22): Fix of review iteration 30 (1 remark; fixes/fix-iter-30.md). One `omn` block changed: INV-079 (one conjunct added). No value, axiom, conformance level, Realises field, declared name, level-annotated attribute declaration, or Elements or Invariants column of the traceability table changed. Every v29 conjunct of INV-079, among them `(∀ d ∈ l.duration • startOf(ctx, l.treatment) ≠ ∅)` of v28, the `omn` block of E-055 (its `when` clauses and the comment of `duration`) and every other formal block that the watch points of the oscillation check after iteration 28 name are byte-identical.
- v31 (iteration 31, 2026-10-22): Fix of review iteration 31 (1 remark; fixes/fix-iter-31.md). Four `omn` blocks changed and four added: the conjuncts of INV-050, INV-062, INV-070 and INV-092 that state what their element is were moved, verbatim, to four new definitional invariants, INV-112 to INV-115. No conjunct was reworded, and no value, axiom, `when` clause, course-event date, declared name, level-annotated attribute declaration or Elements column of the traceability table changed. No element or invariant was withdrawn or renumbered. Section 2.8, E-008's `omn` block, `originalStart`, `resumes`, `courseBegunBy`, INV-001's predicate, the E-049 `omn` block and every other formal block that the watch points of the oscillation check after iteration 28 name are byte-identical.
- v32 (iteration 32, 2026-10-22): Fix of re-check 32b (3 remarks; fixes/fix-iter-32.md). Nine `omn` blocks changed (E-023, E-025, INV-027, INV-039, INV-069, INV-079, INV-082, INV-085, INV-105) and two added (INV-116, INV-117). No value, axiom, `when` clause, course-event date, level of an existing invariant, level-annotated attribute declaration, or Elements column of the traceability table changed, and no element or invariant was withdrawn or renumbered. The `omn` blocks of E-045 (the six named criteria with their names, components, thresholds, conditions and `alsoRestsOn`, and `namedCriteria`), E-046 (`#L.evaluated = 1`, the `evaluationResult` / `pretreatmentBaseline` pair, `rc.treatment = L.treatment`, the type-scope ties, `UnderlyingKind`, `PeriodValueKind` and `otherValueNamed` in E-045), INV-062, INV-063, INV-064 and INV-114, section 2.8, E-008, INV-001 and every other formal block that the watch points of the oscillation check after iteration 28 name are byte-identical.
- v33 (iteration 33, 2026-10-22): Fix of review 33 (2 remarks; fixes/fix-iter-33.md). Four `omn` blocks changed (E-023, E-025, E-033, INV-082) and none added. No element or invariant was added, withdrawn or renumbered, and no value, axiom, `when` clause, level, level-annotated attribute declaration, Realises field, or Elements or Invariants column of the traceability table changed. The `omn` blocks of INV-039, INV-069 and INV-105, which use `onSameScale` and `inSameForm`, of E-045, E-046, E-057, E-058, INV-062, INV-063, INV-064, INV-085 and INV-112 to INV-117, and every other formal block that the watch points of the oscillation checks after iterations 16, 24, 28 and 32 name are byte-identical; of the blocks those watch points name, only E-023, E-025 (comparability, watch point 3 of the check after iteration 32) and INV-082 (watch point 1) changed, each by one added conjunct (in E-023 and E-025 together with the payload of the other-form tag), every earlier conjunct verbatim.
- v34 (iteration 34, 2026-10-22): Fix of review 34 (1 remark; fixes/fix-iter-34.md). Location text only: no `omn` block changed or added, and no quote, value, axiom, `when` clause, level, level-annotated attribute declaration, Realises field, traceability row or source changed. Every formal block is byte-identical to v33.
- v35 (iteration 35, 2026-10-22): Restructuring of the model (PROCESS.md sections 6a and 8, step 2; `restructure/plan-v35.md`; details in `fixes/fix-iter-35.md`). New: output catalogue and case tables C1–C3 (section 4); generic invariants INV-118 to INV-125 and placement markers (rule W2), into which 38 invariants were merged (section 9); source data tables (section 11); case tables (section 2.11); facts the context does not state (R-MCF, section 3.8); ISS-13. Evidence quotes, design reasons, examples and the search log moved to `RATIONALE.md`. Remark R35-01 and the findings CA-01 to CA-19 of `audits/consistency-audit-v34.md` handled; intended changes of meaning CHG-01 to CHG-07 and the reclassification CHG-R1.
  - Corrected after the equivalence check: see `fixes/fix-iter-35-equivalence.md`.
- v36 (iteration 36, 2026-10-22): Fix of review 36 (3 remarks; details in `fixes/fix-iter-36.md`). No `omn` block changed or added. Quote URLs of `RATIONALE.md` corrected (R36-01); the Conformance, Realises and Evidence fields of invariants that lost conjuncts in v35, with the traceability table, catalogue row OC-08 and the section 9 row of INV-036, aligned with the predicates (R36-02); notation and catalogue prose aligned with the formal text (R36-03).
