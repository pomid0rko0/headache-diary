# Headache diary — formal model of output data (Stage 2)
Version: v02 · Iteration: 02 · Status: under review
Baseline: Stage 1 OUTPUT_REQUIREMENTS.md v18 (converged)

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

The model is written in OMN ("output model notation"), a typed first-order set notation defined in this section. OMN takes the mathematical toolkit of Z (sets, tuples, sequences, free types, abbreviations) and the view of Alloy that instances of element types are atoms related by attributes. OMN is a specification notation only. It has no execution semantics, no storage or encoding, and its element types describe output elements shown to a reader, not data structures. Element types and value types are the notation's records with named attributes (Stage 2 PROCESS.md section 3). OMN text appears in fenced blocks marked `omn`. Everything outside these blocks (Meaning, Reading, comments) is explanatory.

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
- `fun f : T₁ × … × Tₙ → T` declares a **given total function**; `⇸` instead of `→` declares a given partial function whose domain is stated in its comment. `fun f(x₁ : T₁, …, xₙ : Tₙ) : T ≙ e` declares a **defined function**.
- `pred p(x₁ : T₁, …, xₙ : Tₙ) ≙ φ` declares a **defined predicate**, an abbreviation for the formula φ with the parameters substituted.
- `axiom φ` states a fact about given constants and given functions, for example a table of their values. An axiom contains no free variables and refers to no output element; it fixes the meaning of the constants and functions it mentions.

### 2.4 Type expressions

- the primitive types of section 2.8, given sets, and the names of enumerations, variants, value types, element types and abbreviations;
- `opt T`: the subsets of T with at most one member (absent = ∅, present = {x});
- `set T`: the finite subsets of T; `set1 T`: the non-empty finite subsets;
- `seq T`: the finite sequences of members of T, that is, functions from 1..n to T for some n ∈ ℕ; `seq1 T`: the non-empty ones;
- `ℙ T`: all subsets of T, finite or not (used only for parameters of predicates and for the semantic constants of section 3.2);
- `T₁ × T₂`: ordered pairs (x, y); `p.1` and `p.2` are the components;
- `→R`, where R is an element type: references to atoms of R (section 2.5);
- `{c₁, …, cₖ}`: the set of the listed constants of one enumeration or variant, used as a type;
- `{x : T | φ}`: the members of T that satisfy φ. When T is an element type, this is a subset of its atoms.

### 2.5 Element types, atoms, composition and references

- **Atoms.** An instance of the model (an *output structure*) is a set of atoms together with the values of their attributes. Each atom has exactly one most specific, non-abstract element type, and it belongs to that type and to every type that type extends. An element type R used as a term denotes the set of its atoms. An `abstract` type has no atoms except those of its subtypes. Two element types are disjoint unless one extends the other. `extends` is single inheritance; attributes are inherited.
- **Attributes.** Each attribute declaration has the form `a : T [derived] level [when φ]`, with `level` one of `core`, `MUST`, `SHOULD`, `MAY` (section 3.3). Every atom x of the type has a value x.a ∈ T. Different element types may declare attributes with the same name; in `e.a` the attribute is that of the type of e. In `when φ`, `self` denotes the atom and `ctx` the context of the output it belongs to (section 3.2).
- **Typing rule for levels.** An attribute of level `SHOULD` or `MAY`, or of level `MUST` with a `when` clause, has a type of the form `opt T`, `set T` or `seq T`, so that absence is expressible. An attribute of level `core`, or `MUST` without `when`, may have any type.
- **Composition.** An attribute whose type mentions an element type R without `→` holds atoms that are parts of the holder. In this model only `Output.views` and `View.content` are composition attributes. Every `View` atom is part of exactly one `Output` atom, and every `Item` atom is part of exactly one `View` atom. `outputOf(x)` is the output an atom belongs to (an output belongs to itself), and `viewOf(x)` is the view an item is part of (section 5, E-003, E-004).
- **References.** An attribute whose type mentions `→R` holds atoms of R. **Rule W1:** every referenced atom belongs to the same output as the holder. References create no parts. `refs(x)` denotes the set of atoms that the attributes of atom x reference directly.

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
- Thresholds, reference levels and offsets taken from sources are written as numerals in constant definitions. Each is supported by a verbatim quote in the element's Evidence, or by the Stage 1 quote that already contains it (cited by requirement and source ID).

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
  - `fun isWeekSpan : Date × Date → 𝔹`: true if and only if the first date is the first day of a calendar week under the week convention of the output and the second date is `plusDays` of the first by 6. Which weekday begins a week is a presentation choice that Stage 1 does not fix;
  - `fun periodEndFrom : Granularity × Date ⇸ Date`: the last day of the period of the given granularity (E-005) that begins on the given date: for `calendarMonth`, the last day of that month (defined when the date is the first day of a month); for `fourWeekPeriod`, `plusDays(d, 27)`; for `calendarWeek`, `plusDays(d, 6)` (defined when the date begins a calendar week).
- `Duration`: non-negative amounts of time, totally ordered, with `+`. `fun minutes : ℚ → Duration`, `fun hours : ℚ → Duration`, `fun daysLong : ℕ → Duration` (whole days), with `minutes(60) = hours(1)` and `hours(24) = daysLong(1)`. A duration is shown with a unit (rule U1).
- `Text`: reader-facing natural-language text in the language of the output. Texts are compared only by equality.
- `DateSpan`: a span of consecutive days, used in contexts and in items that are not reporting periods; `inSpan(d, r)` holds when d lies in r.

### 2.9 Invariants and their scope

Invariants are named predicates (section 6). Each states its scope in its Conformance field:

- **output** (the default): the predicate is evaluated in each output o separately. A quantifier over an element type, `∀ x : R` or `∃ x : R`, ranges over the atoms of R that belong to o, and `ctx` denotes `ctx(o)`;
- **repertoire**: the predicate quantifies explicitly over `Ctx`, `Rep` and outputs (section 3.2). A quantifier over an element type ranges over all atoms; `parts(o)` restricts to one output;
- **context**: the predicate constrains every admissible context; it has the free variable c of type `OutputContext`.

### 2.10 Type checking

The model is well typed when every name used is declared exactly once (or is a primitive of section 2.8 or a semantic constant of section 3.2); every attribute selection `e.a` is applied to a term whose type declares or inherits a; every argument has the parameter's type or a subtype or subset of it (an atom of an element type matches `→R` and `ℙ R` for R itself or a supertype); constants and tags belong to the expected enumeration or variant; the typing rule for levels (section 2.5) holds; and every partial term is guarded (section 2.6).

## 3. Conformance

### 3.1 Levels

The levels are those of RFC 2119 as clarified by RFC 8174, in upper case: MUST, MUST NOT (absolute requirement or prohibition), SHOULD, SHOULD NOT (recommended or not recommended; a deviation is acceptable only for a valid reason in particular circumstances, understood and weighed), MAY (truly optional). In addition, `core` marks an attribute that is part of an element's identity, and "definitional" marks an invariant that is part of an element's definition (section 3.3).

### 3.2 Conformance target and semantic constants

The conformance target is the diary's **repertoire**: the set of outputs it can produce, each paired with the context it is produced for.

```omn
const Ctx : ℙ OutputContext                     -- the admissible output contexts: every OutputContext value (E-007) that satisfies the context invariants
const Rep : ℙ (OutputContext × Output)          -- the repertoire: (c, o) ∈ Rep when the diary produces output o for context c; c ∈ Ctx
fun ctx : Output → OutputContext                -- the context of an output; (ctx(o), o) ∈ Rep, and no output is paired with two contexts
fun parts : Output → set Element                -- o itself, the views of o, and the items of those views
pred provides(K : ℙ Element) ≙ ∃ p ∈ Rep • ∃ x ∈ parts(p.2) • x ∈ K   -- the diary provides content of kind K somewhere in its repertoire
```

`Output` is the element type of E-002, and `OutputContext` the value type of E-007.

A diary is **MUST-conformant** when its repertoire satisfies every definitional invariant (section 3.3) and every MUST and MUST NOT constraint of this model. It is **fully conformant** when it also satisfies every SHOULD and SHOULD NOT constraint, except where a valid reason in particular circumstances justifies a deviation (RFC 2119); the model does not formalise such reasons. MAY constraints impose nothing: they state that the content is permitted and fix its type and meaning.

### 3.3 How levels attach

1. **Availability of an element kind.** The Conformance field of an element states whether the diary MUST, SHOULD or MAY be able to produce it, and under which applicability condition. Each such statement is formalised by a repertoire invariant named in that field. "K is available when C" means: for every context c ∈ Ctx that satisfies C, some output o with (c, o) ∈ Rep contains an atom of K with the stated content.
2. **Attributes.** For an attribute `a : T level when φ` of type `opt T`, `set T` or `seq T`, the presence constraint "for every atom x of the type for which φ holds, x.a is not empty" holds at the given level. An attribute of level `MUST` without `when`, or of level `core`, is present by typing. `core` marks an attribute that is part of the element's identity: an atom without it would not be an instance of the element. A `core` attribute carries no level of its own; it is present whenever the element is. `MAY` imposes no presence constraint.
3. **Element and attribute levels.** An attribute's level applies to every atom of the element that exists. An element whose availability is SHOULD or MAY has MUST attributes only where a MUST statement part of Stage 1 requires that content in every such element; the attribute then cites that part (for example the reporting period of OUT-001, which every summary output MUST state).
4. **Invariants.** Each invariant has one level. An invariant of level MUST NOT or SHOULD NOT has a predicate of the form `¬ F`; F is the prohibited situation, and the invariant is satisfied when F does not occur.
5. **Definitional invariants.** An invariant that states the relation of a derived attribute to other output elements, a bound that follows from an element's definition (for example a number of days within a period), or the structure of an element (for example that a series is consecutive) is *definitional*. It is part of the meaning of the element: an atom that does not satisfy it is not an instance of the element. A definitional invariant has no level of its own. It holds wherever the element is shown, and the level of the element or attribute decides whether the element is shown at all. It therefore cannot make an element more or less required; it excludes only outputs that show a value contradicting the definition of the element, which no Stage 1 requirement permits. Definitional invariants are marked "definitional" in their Conformance field, with the requirement whose element they define.
6. **Stage 1 strength.** Every level follows the strength of the Stage 1 statement part that the element, attribute or invariant realises (Stage 2 PROCESS.md section 4). A prohibition that is the negative form of a Stage 1 statement part or caveat (for example "supports but does not replace clinical assessment and diagnosis", or "reports scores as screening results, not as psychiatric diagnoses") has the negative level of the same strength: SHOULD NOT for a SHOULD part, MUST NOT for a MUST part. A constraint is stronger than one part only where another part of at least that strength directly requires it, and it then cites both parts. Purely structural primitives take the level of the requirement that needs them.

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

### 3.5 Conditions of applicability

- A `when` clause and the antecedent of an invariant refer only to the output context (`ctx` or a context variable: audience, subject properties, the selected time range and periods), to `provides(K)`, and to other output elements. Subject properties are stated as Stage 1 states them ("the subject has migraine", "the subject menstruates"). How they become known is outside the model. They are not decision logic over input data.
- **Reference rule.** Where a Stage 1 statement includes another requirement's output by its ID (for example "migraine days (OUT-005)" in OUT-021), the component keeps the applicability condition of that requirement ("for patients with migraine"). Where a statement names a measure without such a reference (OUT-018, OUT-022, OUT-028, OUT-035), the model adds no condition that the statement does not state (see ISS-03 in section 8).
- **"Where provided".** Stage 1 phrases such as "where the corresponding outputs are provided" (OUT-021), "where OUT-010 is provided" (OUT-029) and "where reported" (OUT-018) are written `provides(K)`.
- **Audiences.** The Audience line of a Stage 1 requirement is stated in the element's Meaning. It adds no constraint unless the Statement itself names an audience-specific output (OUT-025, OUT-034, OUT-035, OUT-036).

### 3.6 Summary outputs

Every `View` (E-003) is a summary output in the sense of OUT-001 and OUT-038: each view summarises diary information for a stated period.

### 3.7 Open world

An output may contain content that the model does not describe. Such content is an atom of `OtherItem` (E-004), so that the prohibitions of section 6, which constrain the `claims` of every element (E-001), apply to it as well. The model constrains what must, should or may be shown and what must not or should not be shown. It does not forbid other content.

## 4. Model overview

The model has five layers.

1. **Frame** (E-001 to E-009). An `Output` is what a reader receives. It consists of one or more `View`s (summary outputs). Each view covers a reporting `Period` and contains `Item`s. Every element carries the `claims` it puts to the reader, which the prohibitions constrain. Every output is produced for an `OutputContext`: the audience, the subject profile (headache types, menstruation, age group, treatments and their course, availability of instrument results), the as-of date, the selected time range and granularity, and selected comparison periods. The repertoire `Rep` pairs outputs with contexts; availability requirements are statements about `Rep`.
2. **Labels and reliability** (E-010, E-011, E-013). `Annotation`s (caveats, prompts, exploratory labels) qualify elements. `DefinitionLabel`s name the published definition of a measure. A `CompletenessIndicator` accompanies each reporting period.
3. **Per-period values** (E-012, E-014 to E-033). A `PeriodValue` is a value shown for one period and one type scope (all headache types combined, or one type): day counts (headache, migraine, moderate/severe, headache-free, symptom-free, acute-medication, functional-impact days), event counts (attacks, auras), intensity, duration, associated symptoms, the most bothersome symptom, caregiver impact, the medication-overuse indicator and composite indices.
4. **Views over time and treatment views** (E-034 to E-056). Series of consecutive periods with treatment markers (time course, weekly medication view, three-month pattern view), period comparisons, the preventive response comparison with its changes, evaluation time points, residual burden, responder labels and adherence, the treatment review view, post-stop monitoring, the withdrawal follow-up view, acute-treatment effectiveness with per-attack lines, the treatment history and scheme windows.
5. **Instruments, special populations and audience-specific views** (E-057 to E-067). Instrument and screening results with their value sets, the menstrual-relation view, cluster-headache outputs, the trigger co-occurrence view, the clinician-facing summary and the patient-facing overview.

Relations among the main kinds (→ is a reference, ⊂ is "part of"):

```
Output ⊃ View ⊃ Item
View.covers → Period;  PeriodValue.period → Period;  Series.periods → Period
Change.reference, Change.compared → DayCount
ResponseComparison → Period (baseline, on-treatment), DayCount, Change, EvaluationTimePoint
ResidualBurden → Change, DayCount;  ResponderLabel → ResponseComparison, ResidualBurden, Period, Item
MedicationOveruseIndicator → Period (reporting period, span), DayCount (basis)
AcuteTreatmentSummary → Period, TreatedAttackLine;  OutcomeSummary → AcuteTreatmentSummary
TreatmentHistoryView ⊃ ClassGroup → TreatmentLine → ResponseComparison | AcuteTreatmentSummary | AdherenceSummary
InstrumentResult → InstrumentResult (baseline administration)
Annotation → Element (qualified);  DefinitionLabel names the definition of a measure shown in its view
```

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
```
- Meaning: The root of all output elements. `claims` states, abstractly, what an element asserts to its reader beyond the values it shows, for example that its content is a diagnosis. The claims that Stage 1 forbids or discourages are enumerated so that the prohibitions can be stated (INV-013, INV-021, INV-043, INV-048, INV-065, INV-084, INV-101, INV-106, INV-107). An empty `claims` set is the normal case.
- Conformance: structural; `claims` is core. The prohibitions carry their own levels (MUST NOT, SHOULD NOT).
- Realises: OUT-003, OUT-011, OUT-016, OUT-018, OUT-020, OUT-023, OUT-028, OUT-033, OUT-038
- Evidence: Stage 1 OUT-003, OUT-011 (Caveats), OUT-016, OUT-018 (Caveats), OUT-020, OUT-023 (Caveats), OUT-028, OUT-033 (Caveats), OUT-038.
- Notes: The claim values exist only so that prohibitions can name them; no Stage 1 requirement asks for any claim to be made.

### E-002 Output
- Definition:
```omn
element Output extends Element {
  views : set1 View  core       -- the views the reader receives together (composition)
}
fun outputOf(x : Element) : Output   -- the output an element belongs to (an output belongs to itself)
```
- Meaning: What one reader receives at one time (for example a consultation summary, a chart or a report), produced for one context (`ctx(o)`, section 3.2).
- Conformance: structural.
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
fun viewOf(x : Item) : View                     -- the view an item is part of
```
- Meaning: A summary output (section 3.6): a coherent presentation of diary information for a stated reporting period, such as a chart, a table, a summary or an overview. Items shown "together", "next to" or "in the same view" are parts of the same view. `qualities` lists the presentation qualities that Stage 1 requires of particular views (plain language, OUT-035; concise, OUT-034).
- Conformance: `covers` MUST for every view (OUT-001: every summary output states its reporting period). The view kinds and their availability are given in the elements that extend View.
- Realises: OUT-001, OUT-034, OUT-035, OUT-038
- Evidence: Stage 1 OUT-001, OUT-034, OUT-035, OUT-038.
- Notes: Relations: INV-003. `plainLanguage` and `concise` are declared qualities of the wording; whether wording is plain or concise is judged by readers and is not further formalised (Stage 1 states no measurable criterion).

### E-004 Item and OtherItem
- Definition:
```omn
abstract element Item extends Element { }
element OtherItem extends Item {
  description : Text  core      -- content the model does not describe further
}
```
- Meaning: `Item` is anything shown inside a view. `OtherItem` is content outside the model's element types (section 3.7), so that prohibitions apply to it.
- Conformance: structural.
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
- Conformance: MUST: every period that an output shows states start, end and length (OUT-001). Because the length is always stated, the number of days in each calendar month is visible (OUT-001 Caveat).
- Realises: OUT-001
- Evidence: Stage 1 OUT-001.
- Notes: Relations: INV-002 (length agrees with the dates; kind agrees with the dates).

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
```
- Meaning: A time series of consecutive reporting periods of one granularity (calendar months, 28-day periods or calendar weeks), used whenever values are shown "for every period in the selected time range" or "as a time series of consecutive reporting periods". `containsPeriodOf(r, g)` holds when the span r contains a whole period of granularity g: a whole calendar month, 28 consecutive days, or a whole calendar week.
- Conformance: structural; it takes the level of the views that use it.
- Realises: OUT-001, OUT-004, OUT-009, OUT-015, OUT-028
- Evidence: Stage 1 OUT-001, OUT-004, OUT-009, OUT-015, OUT-028.
- Notes: Relations: INV-004. `containsPeriodOf` is used in INV-104: a series of periods within a covered period exists only when the covered period contains at least one whole period.

### E-007 OutputContext
- Definition:
```omn
value OutputContext {
  audience : Audience                     -- the reader the output is produced for
  subject : SubjectProfile                -- the person the output is about (E-008)
  asOf : Date                             -- the date as of which the output is produced
  timeRange : DateSpan                    -- the time range selected for the output
  granularity : Granularity               -- the period granularity selected for series
  comparedSpans : seq DateSpan            -- periods selected for comparison (may be empty)
  previousConsultation : opt Date         -- the date of the subject's previous consultation, if any
  schemeSelection : opt SchemeSelection   -- evaluation windows of a reimbursement or monitoring scheme selected by a clinician
  weeklyGranularityRelevant : 𝔹           -- weekly granularity is clinically relevant for this output
}
enum Audience ::= adultPatient | parentOrCaregiver | primaryCareClinician | headacheSpecialist | researcherOrRegistry
const Clinicians : set Audience ≙ {primaryCareClinician, headacheSpecialist}
value SchemeSelection { scheme : SchemeName; windows : seq1 DateSpan }
given SchemeName                          -- the name of a national reimbursement or monitoring scheme, as an output labels it
```
- Meaning: The context for which an output is produced: who reads it, whom it is about, as of which date, for which selected time range and granularity, and which periods or windows the reader selected. Stage 1 refers to these as the selected time range (OUT-004), a period chosen by the clinician (OUT-034), periods to be compared (OUT-001), and evaluation windows selected by the clinician (OUT-025). `weeklyGranularityRelevant` is the OUT-009 condition "where weekly granularity is clinically relevant (tension-type headache, cluster headache, early onset of effect)". Audiences are those of Stage 1 section 2; clinicians preparing reimbursement documentation and paediatric clinicians are clinicians.
- Conformance: structural (a semantic parameter, not an output element). Context invariants: INV-001.
- Realises: OUT-001, OUT-004, OUT-009, OUT-025, OUT-034, OUT-035, OUT-036
- Evidence: Stage 1 section 2 (Audiences), OUT-001, OUT-004, OUT-009, OUT-025, OUT-034.

### E-008 SubjectProfile
- Definition:
```omn
value SubjectProfile {
  headacheTypes : set HeadacheType               -- the headache types the subject has
  possibleHeadacheTypes : set HeadacheType       -- the headache types the subject has or may have
  menstruates : 𝔹
  ageGroup : AgeGroup
  preventiveTreatments : set Treatment
  acuteTreatments : set Treatment
  preventiveTypes : set (Treatment × PreventiveTreatmentType)   -- how current guidance classifies each preventive treatment
  acuteMedications : set AcuteMedication         -- the acute medications (drug and formulation) the subject uses
  courseEvents : set CourseEvent                 -- start, dose changes, target dose, treatment cycles and stop of each treatment
  withdrawalStart : opt Date                     -- start of withdrawal of overused medication, for a subject who is withdrawing
  ihsQ6ChronicAlternative : 𝔹                    -- the IHS 2024 Q6 situation of chronic migraine without a ≥ 50% decrease after multiple preventive options
  instrumentAdministrations : set InstrumentAdministration   -- results of validated instruments that are available
  screeningAdministrations : set ScreeningAdministration     -- results of comorbidity screening instruments that are available
}
enum AgeGroup ::= adult | childOrAdolescent
given Treatment, Drug, FormulationOrRoute
fun drugOf : Treatment → Drug                    -- the medication of a treatment course
value AcuteMedication { drug : Drug; formulation : FormulationOrRoute }
value CourseEvent { treatment : Treatment; kind : CourseEventKind; date : Date }
variant CourseEventKind ::= start | doseChange ⟨DoseChangeDirection⟩ | targetDoseReached
  | cycleEnd ⟨ℕ₁⟩ | stop ⟨StopKind⟩
enum DoseChangeDirection ::= increase | reduction
enum StopKind ::= discontinued | paused
enum PreventiveTreatmentType ::= doseTitratedPreventive | fixedDosePreventive | cgrpInhibitor
  | antiCGRPMonoclonalAntibody | monthlyInjectable | quarterlyInjectable | onabotulinumtoxinA | otherPreventive
value InstrumentAdministration { instrument : Instrument; date : Date }
value ScreeningAdministration { instrument : ScreeningInstrument; date : Date }
pred hasType(c : OutputContext, t : ICHD3Code) ≙ ∃ h ∈ c.subject.headacheTypes • h ⊑ t
pred mayHaveType(c : OutputContext, t : ICHD3Code) ≙ ∃ h ∈ c.subject.possibleHeadacheTypes • h ⊑ t
pred eventOn(c : OutputContext, t : Treatment, k : CourseEventKind, d : Date) ≙
  CourseEvent(treatment ↦ t, kind ↦ k, date ↦ d) ∈ c.subject.courseEvents
fun startOf(c : OutputContext, t : Treatment) : set Date ≙
  {e ∈ c.subject.courseEvents | e.treatment = t ∧ e.kind = start • e.date}     -- at most one member (INV-001)
```
- Meaning: The properties of the output's subject on which Stage 1 conditions depend, stated as Stage 1 states them: the headache types the subject has, or has or may have (OUT-005, OUT-012, OUT-013, OUT-029, OUT-031, OUT-037); whether the subject menstruates (OUT-030, OUT-035); whether the subject is a child or adolescent (OUT-036); the preventive and acute treatments, their course (start, dose change, the date the target or tolerated dose was reached, the end of treatment cycles, stop or pause) and their guidance type (OUT-009, OUT-018, OUT-022, OUT-023, OUT-024, OUT-039); the start of withdrawal of overused medication (OUT-017); and which instrument and screening results are available (OUT-026, OUT-033, OUT-036). A dose reduction (`doseChange(reduction)`) is the "reduced" of OUT-022 and a pause (`stop(paused)`) its "paused". How these properties become known is outside the model.
- Conformance: structural (a semantic parameter). Context invariants: INV-001.
- Realises: OUT-005, OUT-009, OUT-012, OUT-013, OUT-017, OUT-018, OUT-020, OUT-022, OUT-023, OUT-024, OUT-026, OUT-029, OUT-030, OUT-031, OUT-033, OUT-036, OUT-037, OUT-039
- Evidence: Stage 1 statements of the requirements listed. `ihsQ6ChronicAlternative` is the condition of the IHS Q6 statement quoted in E-045.
- Notes: `PreventiveTreatmentType` lists the treatment types to which the guidance time points of E-041 refer (Stage 1 OUT-018: "which differ by treatment type"). `cgrpInhibitor` is the NICE CG150 term; `monthlyInjectable` and `quarterlyInjectable` are the IHS 2024 Q2 categories; a treatment may have several types. Every preventive treatment has at least one type (INV-001): `otherPreventive` is the type of a preventive treatment that none of the other values describes. The guidance rules that apply to all preventive types (E-041) therefore apply to every preventive treatment. A treatment has at most one start, and none of its other course events (dose changes, the date the target dose was reached, cycle ends, stop or pause) precedes its start (INV-001).

### E-009 ICHD-3 code references
- Definition:
```omn
given ICHD3Code
type HeadacheType == ICHD3Code
fun label : ICHD3Code → Text                  -- the code and its name as printed in ICHD-3
fun _⊑_ : ICHD3Code × ICHD3Code → 𝔹           -- h ⊑ t: h is t or a subtype of t in the ICHD-3 code hierarchy
const c1, c1_2, c1_3, c2, c2_3, c3_1, c8_2, c8_2_1, c8_2_2, c8_2_3, c8_2_4, c8_2_5, c8_2_6, c8_2_7, c8_2_8 : ICHD3Code
axiom label(c1) = "1. Migraine" ∧ label(c1_2) = "1.2 Migraine with aura" ∧ label(c1_3) = "1.3 Chronic migraine" ∧
  label(c2) = "2. Tension-type headache (TTH)" ∧ label(c2_3) = "2.3 Chronic tension-type headache" ∧
  label(c3_1) = "3.1 Cluster headache" ∧ label(c8_2) = "8.2 Medication-overuse headache (MOH)" ∧
  label(c8_2_1) = "8.2.1 Ergotamine-overuse headache" ∧ label(c8_2_2) = "8.2.2 Triptan-overuse headache" ∧
  label(c8_2_3) = "8.2.3 Non-opioid analgesic-overuse headache" ∧ label(c8_2_4) = "8.2.4 Opioid-overuse headache" ∧
  label(c8_2_5) = "8.2.5 Combination-analgesic-overuse headache" ∧
  label(c8_2_6) = "8.2.6 Medication-overuse headache attributed to multiple drug classes not individually overused" ∧
  label(c8_2_7) = "8.2.7 Medication-overuse headache attributed to unspecified or unverified overuse of multiple drug classes" ∧
  label(c8_2_8) = "8.2.8 Medication-overuse headache attributed to other medication"
axiom ∀ h, k, t : ICHD3Code • h ⊑ h ∧ (h ⊑ k ∧ k ⊑ h ⇒ h = k) ∧ (h ⊑ k ∧ k ⊑ t ⇒ h ⊑ t)
axiom c1_2 ⊑ c1 ∧ c1_3 ⊑ c1 ∧ c2_3 ⊑ c2 ∧ c8_2_1 ⊑ c8_2 ∧ c8_2_2 ⊑ c8_2 ∧ c8_2_3 ⊑ c8_2 ∧ c8_2_4 ⊑ c8_2 ∧
  c8_2_5 ⊑ c8_2 ∧ c8_2_6 ⊑ c8_2 ∧ c8_2_7 ⊑ c8_2 ∧ c8_2_8 ⊑ c8_2
```
- Meaning: References to ICHD-3 diagnoses by code, with the code labels exactly as ICHD-3 prints them. Headache types of the subject are ICHD-3 codes. `⊑` is the code hierarchy (reflexive and transitive). "The subject has migraine" is `hasType(c, c1)`, "migraine with aura" `hasType(c, c1_2)`, "cluster headache" `hasType(c, c3_1)`, "tension-type headache" `hasType(c, c2)`.
- Conformance: structural.
- Realises: OUT-005, OUT-012, OUT-013, OUT-014, OUT-016, OUT-028, OUT-029, OUT-031, OUT-037
- Evidence: Stage 1 OUT-014, OUT-016, OUT-028 (codes named). Code labels not quoted in Stage 1:
  - [S-001] "1. Migraine", "1.2 Migraine with aura", "1.3 Chronic migraine", "2. Tension-type headache (TTH)", "2.3 Chronic tension-type headache" (classification list, p. 8)
  - [S-001] "3.1 Cluster headache" (classification list, p. 9)
  - [S-001] "8.2 Medication-overuse headache (MOH)", "8.2.1 Ergotamine-overuse headache", "8.2.2 Triptan-overuse headache", "8.2.3 Non-opioid analgesic-overuse headache", "8.2.4 Opioid-overuse headache", "8.2.5 Combination-analgesic-overuse headache", "8.2.6 Medication-overuse headache attributed to multiple drug classes not individually overused", "8.2.7 Medication-overuse headache attributed to unspecified or unverified overuse of multiple drug classes", "8.2.8 Medication-overuse headache attributed to other medication" (classification list, p. 12)
- Notes: The hierarchy axioms follow the code numbering of the classification list. Diagnostic criteria are not restated. `c8_2_7` is listed only to make explicit that OUT-016 does not refer to it.

### 5.2 Labels, caveats and per-period values

### E-010 Annotation
- Definition:
```omn
element Annotation extends Item {
  kind : AnnotationKind  core
  qualifies : set1 →Element  core     -- the view or the items of the same view that the annotation qualifies
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
- Conformance: structural; each kind is required by the invariant that names it (INV-020, INV-047, INV-052, INV-090, INV-092, INV-098, INV-099, INV-100). `exploratoryMeasure` for OUT-008 measures is MAY (E-020 to E-022).
- Realises: OUT-008, OUT-011, OUT-016, OUT-017, OUT-032, OUT-036, OUT-037, OUT-038
- Evidence: Stage 1 statements of the requirements listed; OUT-036 Caveats.
- Notes: Relations: INV-007 (an annotation is shown in the same view as what it qualifies).

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
pred isMeasure(m : PeriodValue, lm : LabelledMeasure) ≙
  (lm = headacheDaysMeasure ∧ m ∈ HeadacheDays) ∨ (lm = migraineDaysMeasure ∧ m ∈ MigraineDays) ∨
  (lm = moderateSevereHeadacheDaysMeasure ∧ m ∈ ModerateSevereHeadacheDays) ∨ (lm = attacksMeasure ∧ m ∈ AttackCount)
```
- Meaning: States which published definition a view follows for headache days, migraine days, moderate/severe headache days or attacks, for example ICHD-3 "Definitions of terms" [S-001], the IHS trial guidelines [S-002][S-003] or the 2026 eDelphi consensus definition of a migraine day [S-043]. For clinicians and researchers.
- Conformance: SHOULD, for each of these measures shown in a view (INV-008). For headache days the label names ICHD-3 (MUST, INV-009); for attacks it names ICHD-3 "frequency of attacks" (SHOULD, INV-010).
- Realises: OUT-002, OUT-004, OUT-005, OUT-006, OUT-007, OUT-028
- Evidence: Stage 1 OUT-002, OUT-004, OUT-005, OUT-006, OUT-007, OUT-028.
- Notes: `PublishedDefinition` is a given set because Stage 1 names examples, not a closed list.

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
```
- Meaning: A value shown for one reporting period. `typeScope` is `allTypes` for values over all headache types combined and `ofType(t)` for the separate presentation per headache type of OUT-029. `concerns(c, sc, t)` holds when a value with scope sc concerns headache type t: it is scoped to t or a subtype, or it covers all types of a subject whose types all fall under t (used for "for migraine", "for tension-type headache", "for cluster headache").
- Conformance: structural; every value refers to its period (OUT-001: every measure states the period it refers to).
- Realises: OUT-001, OUT-029, OUT-037
- Evidence: Stage 1 OUT-001, OUT-029.
- Notes: Relations: INV-003 (the period is shown in the same view).

### E-013 CompletenessIndicator
- Definition:
```omn
element CompletenessIndicator extends PeriodValue {
  expressions : set1 CompletenessExpression  derived core    -- how completely the period is covered, in one or both forms
}
variant CompletenessExpression ::= coveredDays ⟨ℕ⟩           -- days of the period covered by diary information; unit: days
  | proportionCovered ⟨Percent⟩                              -- proportion of the period's days covered by diary information; unit: %
```
- Meaning: How completely a reporting period is covered by diary information, shown next to the summary measures of that period so that readers can judge their reliability. For clinicians, researchers and patients.
- Conformance: SHOULD for each reporting period of a view that shows summary measures (INV-011). SHOULD NOT: presenting a fixed completeness cut-off as clinically validated (INV-013).
- Realises: OUT-003
- Evidence: Stage 1 OUT-003.
- Notes: Relations: INV-012 (covered days do not exceed the period length; a proportion shown with the covered days is `100 × coveredDays ÷ lengthDays`; scope all types). Stage 1 gives the proportion of days as an example; the model admits the number of covered days, the proportion, or both. The 80 % working-group figure and trial exclusion rules are not clinical cut-offs (OUT-003 Caveats); the model states none.

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
  {m ∈ v.content ∩ DayCount | m.measure = k ∧ m.period = p ∧ m.typeScope = sc • m.days}   -- at most one member (INV-006)
```
- Meaning: A number of days within a reporting period, of one kind. The kinds are specified in E-015 to E-018, E-020, E-021, E-029 and E-030.
- Conformance: structural; each kind has its own conformance.
- Realises: OUT-004, OUT-005, OUT-006, OUT-008, OUT-014, OUT-020, OUT-027
- Evidence: Stage 1 statements of the requirements listed.
- Notes: Relations: INV-005 (a number of days does not exceed the period length), INV-006 (one value per measure, period and scope in a view), INV-024, INV-030, INV-031. The value is obtained from diary information; how is out of scope.

### E-015 HeadacheDays
- Definition:
```omn
type HeadacheDays == {m : DayCount | m.measure = headacheDays}
```
- Meaning: The number of headache days in the reporting period, with "headache days" as defined in ICHD-3 "Definitions of terms" [S-001]. For patients, primary-care clinicians, specialists and researchers.
- Conformance: MUST be available for every period of the selected time range, at calendar-month or 28-day granularity (INV-014); its definition label SHOULD be shown (INV-008) and, when shown, names ICHD-3 (INV-009).
- Realises: OUT-001, OUT-002, OUT-004
- Evidence: Stage 1 OUT-001, OUT-002, OUT-004.

### E-016 MigraineDays
- Definition:
```omn
type MigraineDays == {m : DayCount | m.measure = migraineDays}
```
- Meaning: The number of migraine days in the reporting period (monthly migraine days for calendar months or 28-day periods), under the published definition named by the view's definition label. For patients, clinicians and researchers.
- Conformance: MUST be available for every period of the selected time range for patients with migraine, `hasType(ctx, c1)` (INV-015); its definition label SHOULD be shown (INV-008).
- Realises: OUT-001, OUT-002, OUT-005
- Evidence: Stage 1 OUT-001, OUT-002, OUT-005.

### E-017 ModerateSevereHeadacheDays
- Definition:
```omn
type ModerateSevereHeadacheDays == {m : DayCount | m.measure = moderateSevereHeadacheDays}
```
- Meaning: The number of days in the reporting period with headache of moderate or severe intensity, under the definition named by the view's definition label. For clinicians, researchers and patients.
- Conformance: SHOULD be available per reporting period (INV-016); definition label SHOULD (INV-008).
- Realises: OUT-002, OUT-006
- Evidence: Stage 1 OUT-002, OUT-006.

### E-018 MigraineOrModerateSevereHeadacheDays
- Definition:
```omn
type MigraineOrModerateSevereHeadacheDays == {m : DayCount | m.measure = migraineOrModerateSevereHeadacheDays}
```
- Meaning: The number of days in the reporting period with migraine or moderate-to-severe headache, the single count on which the control levels of the IHS position statement 2025 rest. For clinicians and patients.
- Conformance: SHOULD be shown with every responder label that applies the IHS position statement 2025 control levels (INV-062); no availability of its own.
- Realises: OUT-020
- Evidence: Stage 1 OUT-020 (the named criterion "IHS position statement 2025 control levels" and the requirement to show the values it rests on). The count on which the control levels rest:
  - [S-010] "Modest Control. This is defined as four to six days with migraine or moderate-to-severe headache per month." (section "Setting goals of migraine burden while on treatment", p. 6)
- Notes: Relations: INV-031 (it lies between the larger of the migraine-day and moderate/severe-day counts and their sum). See ISS-05.

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
- Meaning: The number of attacks (frequency of attacks as defined in ICHD-3 "Definitions of terms" [S-001]) or of auras (E-027) in the reporting period, shown as a value of its own, separately from headache or migraine days. For clinicians and researchers.
- Conformance: attacks SHOULD be available per reporting period (INV-017); definition label SHOULD (INV-008, INV-010).
- Realises: OUT-002, OUT-007, OUT-013
- Evidence: Stage 1 OUT-002, OUT-007, OUT-013.
- Notes: Being a separate element type from `DayCount`, an attack count is never merged with a day count ("separately from the number of headache or migraine days"). OUT-007 Caveat (the EMA draft moves the primary endpoint to migraine days) does not constrain the output.

### E-020 HeadacheFreeDays
- Definition:
```omn
type HeadacheFreeDays == {m : DayCount | m.measure = headacheFreeDays}
```
- Meaning: The number of headache-free days in the reporting period, an exploratory measure of residual burden. For patients, clinicians and researchers.
- Conformance: MAY, per reporting period. An `exploratoryMeasure` annotation MAY qualify it. In the clinician-facing summary SHOULD (INV-104; see ISS-04).
- Realises: OUT-008
- Evidence: Stage 1 OUT-008.
- Notes: Relations: INV-031 (headache-free days plus headache days do not exceed the period length). The relation is an inequality because days not covered by diary information are neither (definitions state nothing about them).

### E-021 SymptomFreeDays
- Definition:
```omn
type SymptomFreeDays == {m : DayCount | m.measure = symptomFreeDays}
```
- Meaning: The number of symptom-free days in the reporting period (days free of premonitory, aura, headache and postdromal symptoms, as quoted in Stage 1 OUT-008 from [S-002]), an exploratory measure of residual burden.
- Conformance: MAY, per reporting period; `exploratoryMeasure` annotation MAY. In the clinician-facing summary SHOULD (INV-104; see ISS-04).
- Realises: OUT-008
- Evidence: Stage 1 OUT-008.
- Notes: Relations: INV-031 (a symptom-free day is a headache-free day).

### E-022 MigraineFreePeriodMark
- Definition:
```omn
element MigraineFreePeriodMark extends PeriodValue { }
```
- Meaning: Marks a reporting period without migraine days ("periods without migraine days", migraine freedom), an exploratory measure of residual burden.
- Conformance: MAY; `exploratoryMeasure` annotation MAY. In the clinician-facing summary SHOULD, for the covered period and each period of its series that shows 0 migraine days (INV-104; see ISS-04).
- Realises: OUT-008
- Evidence: Stage 1 OUT-008.
- Notes: Relations: INV-031 (shown for a period exactly when the migraine-day count shown for that period is 0).

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
  | otherIntensitySummary ⟨Text⟩
value LevelDays { level : ScalePoint; days : ℕ }      -- unit: days
```
- Meaning: A summary of headache intensity in the reporting period on a stated scale, for example the distribution of headache days by peak intensity category or an average peak intensity. For clinicians and patients.
- Conformance: SHOULD be available per reporting period and in comparisons between periods (INV-018); `scale` SHOULD. Per headache type SHOULD where provided (INV-029).
- Realises: OUT-010, OUT-021, OUT-029, OUT-035
- Evidence: Stage 1 OUT-010.
- Notes: Relations: INV-032 (levels belong to the scale; each count and the sum of the counts do not exceed the period length and the headache days shown for the same period and scope; the mean lies within the scale). The forms are those Stage 1 gives as examples; `otherIntensitySummary` keeps the list open, as Stage 1 does.

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
- Meaning: A summary of attack or headache duration in the reporting period, for example the median attack duration or the hours with moderate/severe pain per 28 days (`moderateSeverePainTime` with statistic `total` over a 28-day period). `auraDuration` is the aura duration of OUT-013. For clinicians and patients.
- Conformance: SHOULD be available per reporting period (INV-019). SHOULD: a duration summary that covers acutely treated attacks is labelled as influenced by acute treatment (INV-020). SHOULD NOT: such a summary is presented as a stand-alone efficacy measure (INV-021, OUT-011 Caveats).
- Realises: OUT-011, OUT-013
- Evidence: Stage 1 OUT-011, OUT-013.
- Notes: Relations: INV-033 (a total time with moderate/severe pain does not exceed the period length).

### E-025 AssociatedSymptomSummary
- Definition:
```omn
element AssociatedSymptomSummary extends PeriodValue {
  symptom : AssociatedSymptom  core
  presence : SymptomPresence  derived core
}
enum AssociatedSymptom ::= nauseaOrVomiting | photophobia | phonophobia
variant SymptomPresence ::= daysWithSymptom ⟨ℕ⟩ | attacksWithSymptom ⟨ℕ⟩ | otherPresenceSummary ⟨Text⟩
```
- Meaning: The presence of a migraine-associated symptom (nausea/vomiting, photophobia, phonophobia) in the reporting period. For clinicians, researchers and patients.
- Conformance: SHOULD be available per reporting period for migraine, `hasType(ctx, c1)`, for each of the three symptoms (INV-022).
- Realises: OUT-012, OUT-021
- Evidence: Stage 1 OUT-012.
- Notes: Relations: INV-033 (days with the symptom do not exceed the period length; attacks with the symptom do not exceed the attack count shown for the same period and scope). Stage 1 fixes no form of "presence"; the two forms are the natural ones and `otherPresenceSummary` keeps the list open.

### E-026 MostBothersomeSymptomItem
- Definition:
```omn
element MostBothersomeSymptomItem extends PeriodValue {
  symptom : Symptom  core
}
variant Symptom ::= associated ⟨AssociatedSymptom⟩ | otherNonPainSymptom ⟨Text⟩
```
- Meaning: The patient's most bothersome symptom, shown for a reporting period. Its absence at the early time point after treatment is an outcome of E-050.
- Conformance: SHOULD be available across periods for migraine (INV-022).
- Realises: OUT-012, OUT-021
- Evidence: Stage 1 OUT-012.

### E-027 Aura measures
- Definition:
```omn
type AuraCount == {m : EventCount | m.event = auras}
type AuraDuration == {m : DurationSummary | m.kind = auraDuration}
```
- Meaning: The number of auras in the reporting period and their duration, shown separately from headache measures. For clinicians and patients.
- Conformance: MAY, per reporting period, for patients with migraine with aura, `hasType(ctx, c1_2)`.
- Realises: OUT-013
- Evidence: Stage 1 OUT-013.
- Notes: Being separate element kinds, aura values are never merged with headache values.

### E-028 AcuteDrugClass
- Definition:
```omn
enum AcuteDrugClass ::= ergotamine | triptans | nonOpioidAnalgesics | opioids | combinationAnalgesics | otherMedication
fun classCode : AcuteDrugClass → ICHD3Code
axiom classCode(ergotamine) = c8_2_1 ∧ classCode(triptans) = c8_2_2 ∧ classCode(nonOpioidAnalgesics) = c8_2_3 ∧
  classCode(opioids) = c8_2_4 ∧ classCode(combinationAnalgesics) = c8_2_5 ∧ classCode(otherMedication) = c8_2_8
fun classOf : Drug ⇸ AcuteDrugClass      -- the ICHD-3 8.2 class of an acute medication; defined for acute medications
const classesOf826 : set1 AcuteDrugClass ≙ {ergotamine, triptans, nonOpioidAnalgesics, opioids}
const classesOf821to825 : set1 AcuteDrugClass ≙ {ergotamine, triptans, nonOpioidAnalgesics, opioids, combinationAnalgesics}
```
- Meaning: The classes of acute (symptomatic) headache medication as used in ICHD-3 code 8.2 and its subtypes. Each class is shown with the label of its ICHD-3 subtype (`label(classCode(k))`). `classOf` assigns each acute medication to its class. `classesOf826` are the classes whose combined use ICHD-3 8.2.6 refers to.
- Conformance: structural.
- Realises: OUT-014, OUT-016
- Evidence: Stage 1 OUT-014, OUT-016. Details not stated in Stage 1:
  - [S-001] the subtype labels quoted in E-009 (classification list, p. 12)
  - [S-001] "For the purposes of ICHD-3, all non-opioid analgesics are regarded as a single class" (8.2.3 Non-opioid analgesic-overuse headache, comments, p. 123; the text layer breaks "non-opioid" at a line end)
  - [S-001] "Regular intake of any combination of ergotamine, triptans, non-opioid analgesics and/or opioids [...] on a total of ≥10 days/month for >3 months without overuse of any single drug or drug class alone." (8.2.6, diagnostic criterion B, p. 124; the omitted text is a footnote marker; "≥" is a glyph without a text mapping in the PDF text layer)
  - [S-001] "Without overuse of any single drug or drug class alone means that criterion B has not been fulfilled for any of the specific subtypes 8.2.1–8.2.5." (8.2.6, note 2, p. 125)
- Notes: The paracetamol, NSAID, acetylsalicylic-acid and other subforms of 8.2.3 are not separate classes, because ICHD-3 regards all non-opioid analgesics as one class; the individual drugs are shown by the per-drug breakdown (E-029). Stage 1's example label "simple analgesics" is not the ICHD-3 class name; see ISS-02. See ISS-01 on the classes of 8.2.6 (`classesOf826`).

### E-029 AcuteMedicationDays
- Definition:
```omn
variant MedicationScope ::= allAcuteMedication | ofClass ⟨AcuteDrugClass⟩ | ofDrug ⟨Drug⟩ | ofClasses ⟨set1 AcuteDrugClass⟩
type AcuteMedicationDays == {m : DayCount | ∃ s : MedicationScope • m.measure = acuteMedicationDays(s)}
type TotalAcuteMedicationDays == {m : DayCount | m.measure = acuteMedicationDays(allAcuteMedication)}
```
- Meaning: The number of days in the reporting period with acute (symptomatic) headache medication: in total across classes (`allAcuteMedication`), per ICHD-3 8.2 class (`ofClass`), per individual drug (`ofDrug`), and, as the basis of the 8.2.6 indicator, for any medication of a set of classes (`ofClasses(classesOf826)`). For clinicians, patients and researchers.
- Conformance: MUST be available per reporting period: the total, each class of the subject's acute medications and each of their drugs (INV-023). Per calendar week SHOULD (INV-025). Per headache type MUST when the subject has or may have more than one type: the total, each class and each drug (INV-028). `ofClasses(classesOf826)` MUST where the 8.2.6 indicator is shown (INV-045).
- Realises: OUT-014, OUT-015, OUT-016, OUT-029
- Evidence: Stage 1 OUT-014, OUT-015, OUT-016, OUT-029; [S-001] 8.2.6 criterion B quoted in E-028.
- Notes: Relations: INV-024 (the total is at least each class value and at most their sum; a class value is at least each of its drugs' values and at most their sum; the 8.2.6 basis lies between the largest and the sum of the values of its classes). A day with two classes counts once in the total and once in each class, so the total is in general not the sum. See ISS-01 on the basis of the 8.2.6 indicator, and ISS-09 on which acute-medication outputs are presented per headache type.

### E-030 FunctionalImpactDays
- Definition:
```omn
enum ImpactDomain ::= paidWorkOrSchool | householdWork | socialOrLeisure | anyActivity
enum ImpactSeverity ::= affected | missed | impaired | severelyImpaired
type FunctionalImpactDays == {m : DayCount | ∃ d : ImpactDomain; s : ImpactSeverity • m.measure = functionalImpactDays((d, s))}
fun fiDays(d : ImpactDomain, s : ImpactSeverity) : ℙ DayCount ≙ {m : DayCount | m.measure = functionalImpactDays((d, s))}
```
- Meaning: The number of days in the reporting period on which headache affected paid work or school, household work, or social or leisure activities (`affected`), including days with severe functional impairment (`severelyImpaired`), in days per period. For children, school days missed (`missed`) or impaired (`impaired`) in the domain `paidWorkOrSchool`. `anyActivity` is used for days with severe impairment of any activity. For clinicians, patients and researchers; for children, parents and caregivers.
- Conformance: SHOULD be available per reporting period for the three domains and for severe impairment (INV-026), and SHOULD allow comparison with the baseline period, for the three domains and for severe impairment (INV-027). For children, school days missed or impaired SHOULD (INV-096).
- Realises: OUT-027, OUT-036
- Evidence: Stage 1 OUT-027, OUT-036.
- Notes: Relations: INV-005, INV-033 (days missed, impaired or severely impaired in a domain do not exceed the days affected in that domain).

### E-031 CaregiverImpact
- Definition:
```omn
element CaregiverImpact extends PeriodValue {
  impact : CaregiverImpactValue  derived core
}
variant CaregiverImpactValue ::= caregiverLostProductiveDays ⟨ℕ⟩ | otherCaregiverImpact ⟨Text⟩    -- unit of the first: days
```
- Meaning: The impact of a child's or adolescent's headache on parents or caregivers in the reporting period, for example their lost productive time in days. For parents and caregivers, paediatric clinicians and researchers.
- Conformance: SHOULD for children and adolescents (INV-096).
- Realises: OUT-036
- Evidence: Stage 1 OUT-036.
- Notes: Relations: INV-033 (lost productive days do not exceed the period length).

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
axiom (∀ k : AcuteDrugClass • overuseCode(ofClassUse(k)) = classCode(k) ∧ basisScope(ofClassUse(k)) = ofClass(k)) ∧
  overuseCode(combinedUse) = c8_2_6 ∧ basisScope(combinedUse) = ofClasses(classesOf826)
axiom overuseLevel(ofClassUse(nonOpioidAnalgesics)) = 15 ∧
  (∀ k : AcuteDrugClass • k ≠ nonOpioidAnalgesics ⇒ overuseLevel(ofClassUse(k)) = 10) ∧ overuseLevel(combinedUse) = 10
const overuseSpanMonths : ℕ₁ ≙ 3          -- the time span is more than 3 months
```
- Meaning: For one reporting period and one acute-medication class, or for the combined use of the classes of ICHD-3 8.2.6, whether acute medication use reached the level of regular use that the ICHD-3 subtype describes over the time span that subtype refers to. The output shows the subtype, its reference level (10 or 15 days per month) and the time span (more than 3 months), next to the indication, together with the medication days on which it rests. It is worded as a prompt for clinical review of possible medication overuse and is not a diagnosis of medication-overuse headache. For clinicians (primary) and, in plain language, patients.
- Conformance: MUST be available per reporting period (calendar month or 28-day period), for each class of the subject's acute medications and for combined use (INV-044). `code`, `referenceLevel`, `span` and `basis` MUST (OUT-016: the indication refers to the levels of the codes over their time span). The review-prompt annotation MUST (INV-047). MUST NOT: presented as a diagnosis of medication-overuse headache (INV-048). The clinical-interpretation caveat SHOULD (INV-100).
- Realises: OUT-014, OUT-016, OUT-038
- Evidence: Stage 1 OUT-016. Reference levels and time span, not stated in Stage 1:
  - [S-001] "[...] regular overuse of acute or symptomatic headache medication (on 10 or more or 15 or more days/month, depending on the medication) for more than three months." (8.2 Medication-overuse headache, Description, p. 122)
  - [S-001] "[...] regular use of ergotamine on 10 or more days/month for more than three months." (8.2.1, Description, p. 123)
  - [S-001] "[...] regular use of one or more triptans on 10 or more days/month for more than three months." (8.2.2, Description, p. 123)
  - [S-001] "[...] regular use of one or more non-opioid analgesics on 15 or more days/month for more than three months." (8.2.3, Description, p. 123)
  - [S-001] "Regular intake of one or more opioids [...] on ≥10 days/month for >3 months." (8.2.4, diagnostic criterion B, p. 124; the omitted text is a footnote marker; "≥" is a glyph without a text mapping in the PDF text layer)
  - [S-001] "Regular intake of one or more combination-analgesic medications [...] on ≥10 days/month for >3 months." (8.2.5, diagnostic criterion B, p. 124; omitted footnote markers; same note on "≥")
  - [S-001] "Regular overuse, on ≥10 days/month for >3 months, of one or more medications other than those described above, [...] taken for acute or symptomatic treatment of headache." (8.2.8, diagnostic criterion B, p. 125; omitted footnote marker; same note on "≥")
  - [S-001] the 8.2.6 criterion B and note 2 quoted in E-028 (pp. 124–125)
- Notes: Relations: INV-045 (code, level, span and basis agree with the scope; the span consists of consecutive monthly periods ending with the indicated period and is longer than three months; a class indication is `levelReached` exactly when every period of the span has at least the reference level of days), INV-046 (combined use). ICHD-3 expresses the levels per month and does not define the month; the model applies them to calendar months or 28-day periods and the output states which (OUT-001). The reading "on ≥ 10 days/month for > 3 months" as "in every month of a span longer than three months" is the model's; ICHD-3 states that these numbers rest on expert opinion (OUT-016 Caveats). Only the medication-use part of ICHD-3 8.2 is shown; the headache-day criterion of 8.2 is not part of this indicator. Because the basis values are shown medication days, a missing diary day can only make the shown count lower than the true count; the completeness indicator (E-013) shows the coverage of each period. See ISS-01. The indicator is required for all headache types combined, not per headache type; see ISS-09.

### E-033 CompositeIndex
- Definition:
```omn
element CompositeIndex extends PeriodValue {
  index : HeadacheIndexKind  core
  combines : {s : set IndexDimension | #s ≥ 2}  core     -- the dimensions the index combines into one score
  value : ℚ  derived core                               -- unit: as the index defines it
  role : MeasureRole  core                              -- how the output presents the index
  components : set →PeriodValue  SHOULD when concerns(ctx, self.typeScope, c1)   -- the component measures shown with it
}
enum HeadacheIndexKind ::= areaUnderHeadacheCurve | otherHeadacheIndex
enum IndexDimension ::= frequency | intensity | duration
enum MeasureRole ::= primaryRole | secondaryRole | exploratoryRole
pred dimensionOf(m : PeriodValue, d : IndexDimension) ≙
  (d = frequency ∧ m ∈ HeadacheDays ∪ MigraineDays ∪ ModerateSevereHeadacheDays ∪ AttackCount) ∨
  (d = intensity ∧ m ∈ IntensitySummary) ∨ (d = duration ∧ m ∈ DurationSummary)
```
- Meaning: A headache index that multiplies or otherwise combines frequency, intensity and/or duration into one score, including the area under the headache curve (AUC) of the IHS tension-type headache trial guideline (section 2.3.3.2 [S-006]). `role` states whether the output presents it as a primary measure.
- Conformance: no availability (Stage 1 neither requires nor recommends an index). For migraine: SHOULD NOT be presented as a primary measure (INV-091); if shown, SHOULD be labelled exploratory and shown with its component measures (INV-092). For tension-type headache: if AUC is presented as a primary measure, headache days for the same periods SHOULD be shown with it (INV-093).
- Realises: OUT-037
- Evidence: Stage 1 OUT-037.
- Notes: The formula of an index is computed from diary information and is out of scope. Stage 1 OUT-037 covers only migraine and tension-type headache; the model states nothing for other headache types (OUT-037 Caveats).

### 5.3 Views over time and comparisons

### E-034 TreatmentMarker
- Definition:
```omn
element TreatmentMarker extends Item {
  treatment : Treatment  core
  event : CourseEventKind  core     -- start, dose change or stop (discontinued or paused)
  date : Date  core
}
pred markedKind(k : CourseEventKind) ≙ k is start ∨ k is doseChange ∨ k is stop
```
- Meaning: A dated marker in a time-course view for the start, a dose change or the stop of a preventive treatment, so that the onset of effect and the trajectory of response can be related to the treatment course.
- Conformance: SHOULD, for every such event of a preventive treatment within the period a time-course view covers (INV-035).
- Realises: OUT-009
- Evidence: Stage 1 OUT-009.
- Notes: Relations: INV-036 (a marker shows an event of the subject's preventive treatment course, with its date).

### E-035 TimeCourseView
- Definition:
```omn
element TimeCourseView extends View {
  series : →Series  core
  markers : set →TreatmentMarker  SHOULD when ∃ e ∈ ctx.subject.courseEvents •
      e.treatment ∈ ctx.subject.preventiveTreatments ∧ markedKind(e.kind) ∧ self.covers.start ≤ e.date ∧ e.date ≤ self.covers.end
}
```
- Meaning: Frequency measures (headache days, migraine days, moderate/severe headache days, attacks) shown as a time series of consecutive reporting periods (for example a chart of consecutive months or 28-day periods, or of weeks), with dated markers for the start, dose changes and stop of preventive treatments, so that onset of effect, the trajectory of response and spontaneous fluctuation can be seen. For patients, clinicians and researchers.
- Conformance: SHOULD be available at calendar-month or 28-day granularity, and at weekly granularity where weekly granularity is clinically relevant (`ctx.weeklyGranularityRelevant`) (INV-034); content SHOULD (INV-035).
- Realises: OUT-009, OUT-034, OUT-035
- Evidence: Stage 1 OUT-009.

### E-036 WeeklyMedicationView
- Definition:
```omn
type WeeklyMedicationView == {v : View | ∃ sr ∈ v.content ∩ Series •
  sr.granularity = calendarWeek ∧ perPeriod(v, sr, TotalAcuteMedicationDays, allTypes)}
```
- Meaning: Acute-medication days per calendar week, in addition to the per-period totals of E-029, so that use on several days within a week is visible. For clinicians and patients.
- Conformance: SHOULD be available (INV-025).
- Realises: OUT-015
- Evidence: Stage 1 OUT-015.
- Notes: The weekly and monthly limits of IHS Q12 [S-009] belong to that source and are not part of the output (OUT-015 Caveats). The weekly view is required for all headache types combined, not per headache type; see ISS-09.

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
- Conformance: a comparison of selected periods of equal length MUST be available for the frequency measures (INV-037); intensity in comparisons SHOULD (INV-039), for children and adolescents for selections of equal length. For children and adolescents, compared periods SHOULD have equal length (INV-097).
- Realises: OUT-001, OUT-010, OUT-027, OUT-036
- Evidence: Stage 1 OUT-001, OUT-010, OUT-036.
- Notes: Relations: INV-038 (every value refers to one of the compared periods). Equal length is required where OUT-001 asks for it, not for every comparison: calendar months differ in length, and OUT-001 makes the lengths visible instead (OUT-001 Caveats).

### E-038 ThreeMonthPatternView
- Definition:
```omn
element ThreeMonthPatternView extends View {
  series : →Series  core                       -- the three most recent consecutive monthly periods
  referencedCodes : set ICHD3Code  SHOULD      -- the ICHD-3 codes the view refers to
}
pred mostRecent(sr : Series, d : Date) ≙
  last(sr.periods).end ≤ d ∧ d < periodEndFrom(sr.granularity, next(last(sr.periods).end))
```
- Meaning: Headache days and migraine days for each of the most recent three consecutive calendar months or 28-day periods, so that a clinician can relate the pattern to ICHD-3 code 1.3 Chronic migraine (and to 2.3 Chronic tension-type headache where relevant). The view does not itself assign a diagnosis. For clinicians.
- Conformance: MUST be available with headache days and migraine days for each of the three periods (INV-040). SHOULD show the definitions it refers to: definition labels and the referenced codes (INV-042). SHOULD NOT assign a diagnosis (INV-043).
- Realises: OUT-028, OUT-038
- Evidence: Stage 1 OUT-028.
- Notes: Relations: INV-041 (three consecutive monthly periods, the most recent ones ending on or before the as-of date; `periodEndFrom` is defined there because the periods are of the series granularity, INV-002 and INV-004). The ICHD-3 criteria for 1.3 and 2.3 are not shown or restated: the view refers to the codes, and applying the criteria is the clinician's diagnosis. See ISS-03.

### 5.4 Medication overuse and withdrawal

### E-039 WithdrawalFollowUpView
- Definition:
```omn
element WithdrawalFollowUpView extends View {
  withdrawalStart : Date  core
  series : →Series  core                        -- consecutive periods from the start of withdrawal onward
  reviewWindow : opt →Period  derived SHOULD    -- the review window of NICE CG150 rec. 1.3.48
}
const reviewWindowFromWeeks : ℕ₁ ≙ 4
const reviewWindowToWeeks : ℕ₁ ≙ 8
const followUpMonths : ℕ₁ ≙ 12                   -- "over the following year"
```
- Meaning: For a patient withdrawing from overused medication, headache days and acute-medication days from the start of withdrawal onward, including the review window 4 to 8 weeks after the start of withdrawal named in NICE CG150 recommendation 1.3.48, continued over the following year, with a label of the expected transient worsening in the early withdrawal phase. For clinicians and patients.
- Conformance: SHOULD be available for contexts whose subject is withdrawing (`ctx.subject.withdrawalStart ≠ ∅`), for time ranges from the start of withdrawal up to one year after it (INV-049); content SHOULD (INV-050); worsening label SHOULD (INV-052).
- Realises: OUT-017
- Evidence: Stage 1 OUT-017 (the window "4 to 8 weeks after the start of withdrawal" is in the Stage 1 statement and in its quote [S-015] rec. 1.3.48).
- Notes: Relations: INV-051 (the review window starts 4 weeks and ends 8 weeks after the start of withdrawal). "The following year" is read as the 12 months after the start of withdrawal.

### 5.5 Preventive treatment response

### E-040 Change
- Definition:
```omn
element Change extends Item {
  reference : →DayCount  core           -- the value of the reference (baseline) period
  compared : →DayCount  core            -- the value of the compared period
  absolute : ℤ  derived MUST            -- unit: days
  relative : RelativeChange  derived MUST
}
variant RelativeChange ::= percent ⟨ℚ⟩ | undefinedForZeroReference      -- unit of percent: %
```
- Meaning: The absolute and the percentage change of a day count between a reference (baseline) period and a compared period. When the reference value is 0, a percentage change does not exist, and the output says so.
- Conformance: MUST wherever a response comparison shows a change (E-043); shown together with the two values it compares (INV-054).
- Realises: OUT-018, OUT-019, OUT-020
- Evidence: Stage 1 OUT-018.
- Notes: Relations: INV-053 (`absolute = compared.days − reference.days`; `percent(q)` with `q ≈ 100 × absolute ÷ reference.days` when `reference.days > 0`; same measure and scope).

### E-041 EvaluationRule
- Definition:
```omn
value EvaluationRule {
  guidance : Text                            -- the guidance and recommendation as the output names it
  appliesTo : set1 PreventiveTreatmentType
  anchor : AnchorKind
  timing : TimePointTiming
  minOffset : CalendarOffset
  maxOffset : opt CalendarOffset
}
variant AnchorKind ::= treatmentStartAnchor | toleratedOrTargetDoseAnchor | endOfCycleAnchor ⟨ℕ₁⟩
enum TimePointTiming ::= atOffset | atLeastOffset | withinWindow
variant CalendarOffset ::= weeks ⟨ℕ⟩ | months ⟨ℕ⟩
fun shift : Date × CalendarOffset → Date
axiom ∀ d : Date; n : ℕ • shift(d, weeks(n)) = plusDays(d, 7 × n) ∧ shift(d, months(n)) = plusMonths(d, n)
const allPreventiveTypes : set1 PreventiveTreatmentType ≙ {doseTitratedPreventive, fixedDosePreventive, cgrpInhibitor,
  antiCGRPMonoclonalAntibody, monthlyInjectable, quarterlyInjectable, onabotulinumtoxinA, otherPreventive}
const ruleNice1327, ruleNice1328, ruleNice1329, ruleAan14A, ruleSignTitrated, ruleSignFixedDose, ruleEhf2022Q3, ruleIhsQ2Monthly, ruleIhsQ2Quarterly, ruleNvnTitrated, ruleRu71 : EvaluationRule
axiom
  ruleNice1327 = EvaluationRule(guidance ↦ "NICE CG150 rec. 1.3.27", appliesTo ↦ allPreventiveTypes,
    anchor ↦ treatmentStartAnchor, timing ↦ withinWindow, minOffset ↦ months(3), maxOffset ↦ {months(6)}) ∧
  ruleNice1328 = EvaluationRule(guidance ↦ "NICE CG150 rec. 1.3.28", appliesTo ↦ {cgrpInhibitor},
    anchor ↦ treatmentStartAnchor, timing ↦ atOffset, minOffset ↦ weeks(12), maxOffset ↦ ∅) ∧
  ruleNice1329 = EvaluationRule(guidance ↦ "NICE CG150 rec. 1.3.29", appliesTo ↦ {onabotulinumtoxinA},
    anchor ↦ endOfCycleAnchor(2), timing ↦ atOffset, minOffset ↦ weeks(0), maxOffset ↦ ∅) ∧
  ruleAan14A = EvaluationRule(guidance ↦ "AAN/AHS 2026 rec. 14A", appliesTo ↦ allPreventiveTypes,
    anchor ↦ toleratedOrTargetDoseAnchor, timing ↦ withinWindow, minOffset ↦ weeks(8), maxOffset ↦ {weeks(12)}) ∧
  ruleSignTitrated = EvaluationRule(guidance ↦ "SIGN 155 section 4.1 (titrated treatment)", appliesTo ↦ {doseTitratedPreventive},
    anchor ↦ toleratedOrTargetDoseAnchor, timing ↦ atLeastOffset, minOffset ↦ weeks(8), maxOffset ↦ ∅) ∧
  ruleSignFixedDose = EvaluationRule(guidance ↦ "SIGN 155 section 4.1 (fixed-dose treatment)", appliesTo ↦ {fixedDosePreventive},
    anchor ↦ treatmentStartAnchor, timing ↦ atOffset, minOffset ↦ months(3), maxOffset ↦ ∅) ∧
  ruleEhf2022Q3 = EvaluationRule(guidance ↦ "EHF 2022 guideline, expert consensus statement, question 3", appliesTo ↦ {antiCGRPMonoclonalAntibody},
    anchor ↦ treatmentStartAnchor, timing ↦ atLeastOffset, minOffset ↦ months(3), maxOffset ↦ ∅) ∧
  ruleIhsQ2Monthly = EvaluationRule(guidance ↦ "IHS global practice recommendations Q2 (monthly injectables)", appliesTo ↦ {monthlyInjectable},
    anchor ↦ treatmentStartAnchor, timing ↦ atLeastOffset, minOffset ↦ months(3), maxOffset ↦ ∅) ∧
  ruleIhsQ2Quarterly = EvaluationRule(guidance ↦ "IHS global practice recommendations Q2 (quarterly injectables)", appliesTo ↦ {quarterlyInjectable},
    anchor ↦ treatmentStartAnchor, timing ↦ atLeastOffset, minOffset ↦ months(6), maxOffset ↦ ∅) ∧
  ruleNvnTitrated = EvaluationRule(guidance ↦ "NVN guideline Hoofdpijn, module Profylactische behandeling migraine (titrated prophylactics)",
    appliesTo ↦ {doseTitratedPreventive}, anchor ↦ treatmentStartAnchor, timing ↦ withinWindow, minOffset ↦ months(2), maxOffset ↦ {months(3)}) ∧
  ruleRu71 = EvaluationRule(guidance ↦ "Russian clinical recommendations «Мигрень» (adults) 2024, section 7.1", appliesTo ↦ allPreventiveTypes,
    anchor ↦ treatmentStartAnchor, timing ↦ atOffset, minOffset ↦ months(3), maxOffset ↦ ∅)
const evaluationRules : set1 EvaluationRule ≙ {ruleNice1327, ruleNice1328, ruleNice1329, ruleAan14A, ruleSignTitrated,
  ruleSignFixedDose, ruleEhf2022Q3, ruleIhsQ2Monthly, ruleIhsQ2Quarterly, ruleNvnTitrated, ruleRu71}
pred anchorMatches(a : AnchorKind, k : CourseEventKind) ≙
  (a = treatmentStartAnchor ∧ k = start) ∨ (a = toleratedOrTargetDoseAnchor ∧ k = targetDoseReached) ∨
  (∃ n : ℕ₁ • a = endOfCycleAnchor(n) ∧ k = cycleEnd(n))
fun anchorDates(c : OutputContext, t : Treatment, a : AnchorKind) : set Date ≙
  {e ∈ c.subject.courseEvents | e.treatment = t ∧ anchorMatches(a, e.kind) • e.date}
pred applicable(c : OutputContext, t : Treatment, r : EvaluationRule) ≙
  t ∈ c.subject.preventiveTreatments ∧ (∃ ty ∈ r.appliesTo • (t, ty) ∈ c.subject.preventiveTypes) ∧ anchorDates(c, t, r.anchor) ≠ ∅
```
- Meaning: The evaluation time points named in current guidance, which differ by treatment type: about 8–12 weeks at the tolerated or target dose for most oral preventives, a minimum of 3 consecutive months for anti-CGRP monoclonal antibodies, a minimum of 3 months for monthly and of 6 months for quarterly injectables, 12 weeks for CGRP inhibitors under NICE, 3 months for fixed-dose treatments, 3 to 6 months after starting any prophylaxis, the end of the second treatment cycle for onabotulinumtoxinA, no earlier than after 2–3 months of treatment for titrated prophylactics under the Dutch NVN guideline, and after 3 months of therapy under the Russian clinical recommendations. `atOffset`: the time point is the date `shift(anchor, minOffset)`; `atLeastOffset`: the earliest time point is that date ("a minimum of", "at least"); `withinWindow`: the time point lies between the two offsets.
- Conformance: structural (a value set); its use is MUST (E-042, INV-055, INV-059).
- Realises: OUT-018
- Evidence: Stage 1 OUT-018. Every offset is in a Stage 1 quote of OUT-018: [S-015] recs 1.3.27 ("3 to 6 months after starting"), 1.3.28 ("after 12 weeks of treatment"), 1.3.29 ("after 2 treatment cycles"); [S-018] rec. 14A ("at least 8–12 weeks at the recommended tolerated dose of most medications"); [S-016] section 4.1 ("eight weeks at the target dose or maximum tolerated dose (for those with a titration schedule)"; "For treatments of fixed dose [...] assessed at 3 months"); [S-011] question 3 ("a minimum of 3 consecutive months on treatment"); [S-008] Q2 ("a minimum of three months for injectable drugs taken on a monthly basis, and a minimum of six months for injectable drugs administered quarterly"); [S-028] module "Profylactische behandeling migraine", Aanbeveling ("Titreer naar de ondergrens van de geadviseerde therapeutische breedte" and "evalueer het effect niet eerder dan na 2-3 maanden behandeling"); [S-033] section 7.1 ("через 3 месяца терапии"). The [S-028] and [S-033] fragments are parts of the Stage 1 quotes of OUT-018, whose translations carry over.
- Notes: The rule list is the set of evaluation time points named in the Stage 1 evidence of OUT-018 ([S-015], [S-018], [S-016], [S-011], [S-008], [S-028], [S-033]). Stage 1 gives them as examples ("for example"), so a diary may show further guidance time points as `OtherItem`s. AAN/AHS 14A ("at least 8–12 weeks") is modelled as a window from 8 to 12 weeks after the tolerated dose is reached; "most medications" is modelled as applying to every preventive type. NVN ("niet eerder dan na 2-3 maanden behandeling", no earlier than after 2–3 months of treatment) is modelled in the same way, as a window from 2 to 3 months after the treatment start. It applies to dose-titrated preventives, because the recommendation concerns prophylactics titrated to their therapeutic range ("Titreer naar de ondergrens van de geadviseerde therapeutische breedte"). The Russian section 7.1 time point ("через 3 месяца терапии", after 3 months of therapy) is the time point of the criterion `critRu71` (E-045); the recommendation concerns preventive treatment of migraine in general, so it applies to every preventive type. NICE 1.3.29 is anchored at the end of the second treatment cycle, with no further offset (`weeks(0)`). Every preventive treatment has at least one type (INV-001), so `applicable` holds for the rules of all preventive types whenever the treatment has the rule's anchor. Because no course event precedes the treatment start (INV-001), every rule except NICE 1.3.29 puts its time point at least 8 weeks after the start; the time point of NICE 1.3.29 is the end of the second cycle itself, and where that end is less than 28 days after the start, no calendar month or 28-day period beginning on or after the start can end at it (`fitsMonthlyPeriod`, E-042; INV-055).

### E-042 EvaluationTimePoint
- Definition:
```omn
element EvaluationTimePoint extends Item {
  rule : EvaluationRule  core
  treatment : Treatment  core
  anchorDate : Date  MUST                 -- the treatment start, the date the tolerated or target dose was reached, or the end of a treatment cycle
  earliest : Date  derived MUST
  latest : opt Date  derived MUST when self.rule.maxOffset ≠ ∅
}
pred atTimePoint(p : Period, tp : EvaluationTimePoint) ≙
  (tp.rule.timing ∈ {atOffset, atLeastOffset} ⇒ p.end = tp.earliest) ∧
  (tp.rule.timing = withinWindow ⇒ tp.earliest ≤ p.end ∧ ∀ l ∈ tp.latest • p.end ≤ l)
const shortestMonthlyDays : ℕ₁ ≙ 28          -- the length of a 28-day period; no calendar month is shorter; unit: days
pred fitsMonthlyPeriod(s : Date, a : Date, r : EvaluationRule) ≙
  (r.timing ∈ {atOffset, atLeastOffset} ⇒ plusDays(s, shortestMonthlyDays − 1) ≤ shift(a, r.minOffset)) ∧
  (r.timing = withinWindow ⇒ ∀ x ∈ r.maxOffset • plusDays(s, shortestMonthlyDays − 1) ≤ shift(a, x))
```
- Meaning: An evaluation time point of a guidance rule for one preventive treatment, shown with the response comparison: the guidance it comes from, its anchor date, and the date (or window) on which the evaluation falls. `fitsMonthlyPeriod(s, a, r)` holds when a calendar month or 28-day period that begins on or after the treatment start s can end at the time point of rule r anchored at a (for a window, within the window): such a period has at least 28 days (E-005), so it ends no earlier than 27 days after s.
- Conformance: MUST be shown with each response comparison for every rule applicable to the treatment (INV-059).
- Realises: OUT-018
- Evidence: Stage 1 OUT-018 (see E-041); Stage 1 OUT-001 for the 28-day (4-week) period.
- Notes: Relations: INV-058 (`earliest = shift(anchorDate, rule.minOffset)`; `latest = shift(anchorDate, maxOffset)`; the anchor date is the subject's course event of the rule's anchor kind; the rule applies to the treatment's type). `fitsMonthlyPeriod` is used in INV-055.

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
  timePoints : set →EvaluationTimePoint  MUST when ∃ r ∈ evaluationRules • applicable(ctx, self.treatment, r)
}
```
- Meaning: For one preventive treatment, monthly migraine days and monthly headache days (and, where the diary reports them, moderate/severe headache days) in a pre-treatment baseline month compared with monthly periods after the treatment start, aligned to the treatment start date, showing the values of each period and the absolute and percentage change from baseline, with the guidance evaluation time points. For clinicians, patients and researchers.
- Conformance: MUST be available for each preventive treatment, including a comparison of equal-length periods at each applicable evaluation time point that a monthly on-treatment period can reach (INV-055); content MUST (INV-056, INV-057, INV-059). MUST NOT: a decision on continuing the treatment (INV-106).
- Realises: OUT-001, OUT-018, OUT-036
- Evidence: Stage 1 OUT-001, OUT-018, OUT-036.
- Notes: The baseline and on-treatment periods are calendar months or 28-day periods (INV-056), the monthly periods of OUT-001, so the values compared and their changes are monthly migraine days and monthly headache days, as OUT-018 states. Several consecutive or separate monthly on-treatment periods may be compared with the same baseline month. An on-treatment period begins on or after the treatment start and has at least 28 days, so it cannot end at a time point less than 28 days after the start; INV-055 does not require a comparison at such a time point (`fitsMonthlyPeriod`, E-042), which can arise only for NICE CG150 1.3.29 (E-041 Notes). The comparison shows the change and does not itself decide on continuation (OUT-018 Caveats, INV-106); responder labels are a separate, optional element (E-046). Migraine days are compared without the condition "for patients with migraine", as OUT-018 states them; see ISS-03.

### E-044 ResidualBurden
- Definition:
```omn
element ResidualBurden extends Item {
  change : →Change  core                         -- the relative change it is shown next to
  migraineDays : →DayCount  core                 -- migraine days per month that remain on treatment
  moderateSevereHeadacheDays : →DayCount  core   -- moderate/severe headache days per month that remain on treatment
}
```
- Meaning: Next to a percentage change in migraine or headache days, the absolute numbers of migraine days and of moderate/severe headache days per month that remain on treatment, so that a large percentage reduction does not hide a substantial number of disabling days. For clinicians and patients.
- Conformance: SHOULD, wherever a percentage change in migraine or headache days is shown (INV-060).
- Realises: OUT-019
- Evidence: Stage 1 OUT-019.
- Notes: Relations: INV-061 (the two values are of their measures, with the scope of the change, for a calendar-month or 28-day period: the compared period itself when it is monthly, as in every response comparison, and otherwise a monthly period within it). "Per month" is represented by a monthly period, so no conversion formula is needed. See ISS-05.

### E-045 ResponderCriterion
- Definition:
```omn
value ResponderCriterion {
  name : Text                                    -- the criterion as the output names it
  components : set1 CriterionComponent           -- any one or more of the components makes the criterion met
  alsoRestsOn : set UnderlyingKind               -- values other than frequency on which the criterion rests
}
variant CriterionComponent ::= reductionFromBaseline ⟨ReductionComponent⟩ | scoreDecrease ⟨ScoreComponent⟩
  | judgement ⟨Text⟩ | controlLevels
value ReductionComponent { measures : set1 DayMeasure; atLeastPercent : Percent; condition : SubjectCondition }
value ScoreComponent { instrument : Instrument; decrease : ScoreDecrease; baselineAtLeast : opt ℚ; baselineAtMost : opt ℚ;
  condition : SubjectCondition }
variant ScoreDecrease ::= atLeastPoints ⟨ℚ⟩ | atLeastPercentOfBaseline ⟨Percent⟩
variant SubjectCondition ::= anySubject | episodicMigraineOnly | chronicMigraineOnly | ihsQ6ChronicAlternativeOnly
variant UnderlyingKind ::= instrumentResultOf ⟨Instrument⟩ | acuteTreatmentEffectiveness
pred conditionHolds(c : OutputContext, s : SubjectCondition) ≙
  (s = episodicMigraineOnly ⇒ hasType(c, c1) ∧ ¬ hasType(c, c1_3)) ∧ (s = chronicMigraineOnly ⇒ hasType(c, c1_3)) ∧
  (s = ihsQ6ChronicAlternativeOnly ⇒ c.subject.ihsQ6ChronicAlternative)
pred valueAvailable(c : OutputContext, u : UnderlyingKind) ≙
  (∀ ins : Instrument • u = instrumentResultOf(ins) ⇒ ∃ a ∈ c.subject.instrumentAdministrations • a.instrument = ins) ∧
  (u = acuteTreatmentEffectiveness ⇒ c.subject.acuteMedications ≠ ∅)
const critNice1328, critNice1329, critIhsQ6, critIhs2025, critDmkg, critRu71 : ResponderCriterion
axiom
  critNice1328 = ResponderCriterion(name ↦ "NICE CG150 rec. 1.3.28",
    components ↦ {reductionFromBaseline(ReductionComponent(measures ↦ {migraineDays}, atLeastPercent ↦ 50, condition ↦ episodicMigraineOnly)),
                  reductionFromBaseline(ReductionComponent(measures ↦ {migraineDays}, atLeastPercent ↦ 30, condition ↦ chronicMigraineOnly))},
    alsoRestsOn ↦ ∅) ∧
  critNice1329 = ResponderCriterion(name ↦ "NICE CG150 rec. 1.3.29",
    components ↦ {reductionFromBaseline(ReductionComponent(measures ↦ {headacheDays}, atLeastPercent ↦ 30, condition ↦ anySubject))},
    alsoRestsOn ↦ ∅) ∧
  critIhsQ6 = ResponderCriterion(name ↦ "IHS global practice recommendations Q6",
    components ↦ {reductionFromBaseline(ReductionComponent(measures ↦ {migraineDays, moderateSevereHeadacheDays}, atLeastPercent ↦ 50, condition ↦ anySubject)),
                  reductionFromBaseline(ReductionComponent(measures ↦ {migraineDays, moderateSevereHeadacheDays}, atLeastPercent ↦ 30, condition ↦ ihsQ6ChronicAlternativeOnly)),
                  judgement("a clinically meaningful subjective improvement as reported by the person with migraine or evaluated by Patient Global Impression scales"),
                  scoreDecrease(ScoreComponent(instrument ↦ midas, decrease ↦ atLeastPoints(5), baselineAtLeast ↦ {11}, baselineAtMost ↦ {20}, condition ↦ anySubject)),
                  scoreDecrease(ScoreComponent(instrument ↦ midas, decrease ↦ atLeastPercentOfBaseline(30), baselineAtLeast ↦ {20}, baselineAtMost ↦ ∅, condition ↦ anySubject)),
                  scoreDecrease(ScoreComponent(instrument ↦ hit6, decrease ↦ atLeastPoints(5), baselineAtLeast ↦ ∅, baselineAtMost ↦ ∅, condition ↦ anySubject))},
    alsoRestsOn ↦ {instrumentResultOf(pgic), instrumentResultOf(midas), instrumentResultOf(hit6)}) ∧
  critIhs2025 = ResponderCriterion(name ↦ "IHS position statement 2025 control levels", components ↦ {controlLevels},
    alsoRestsOn ↦ {acuteTreatmentEffectiveness}) ∧
  critDmkg = ResponderCriterion(name ↦ "DMKG/ÖKSG/SKG consensus statement (episodic migraine)",
    components ↦ {reductionFromBaseline(ReductionComponent(measures ↦ {migraineDays}, atLeastPercent ↦ 50, condition ↦ episodicMigraineOnly)),
                  scoreDecrease(ScoreComponent(instrument ↦ hit6, decrease ↦ atLeastPoints(5), baselineAtLeast ↦ ∅, baselineAtMost ↦ ∅, condition ↦ episodicMigraineOnly)),
                  scoreDecrease(ScoreComponent(instrument ↦ midas, decrease ↦ atLeastPercentOfBaseline(30), baselineAtLeast ↦ ∅, baselineAtMost ↦ ∅, condition ↦ episodicMigraineOnly))},
    alsoRestsOn ↦ {instrumentResultOf(hit6), instrumentResultOf(midas)}) ∧
  critRu71 = ResponderCriterion(name ↦ "Russian clinical recommendations «Мигрень» (adults) 2024, section 7.1",
    components ↦ {reductionFromBaseline(ReductionComponent(measures ↦ {headacheDays}, atLeastPercent ↦ 50, condition ↦ anySubject))},
    alsoRestsOn ↦ ∅)
const namedCriteria : set1 ResponderCriterion ≙ {critNice1328, critNice1329, critIhsQ6, critIhs2025, critDmkg, critRu71}
```
- Meaning: A named responder criterion with its thresholds, as an output shows it next to a responder label: a criterion is met when any one of its components is met. `reductionFromBaseline`: a reduction from baseline of at least the stated percentage in one of the listed measures, for subjects meeting the condition; `scoreDecrease`: a decrease of an instrument score of at least the stated points or percentage of the baseline score, for baseline scores in the stated range; `judgement`: a component that rests on a clinical or patient judgement, shown by its wording; `controlLevels`: the four control levels of the IHS position statement 2025 (E-046, INV-064). `namedCriteria` are the criteria named in the Stage 1 evidence of OUT-018 and OUT-020. `valueAvailable(c, u)` holds when a value of kind u on which a criterion also rests can exist for the subject: a result of the instrument is available (the condition of OUT-026, "Where results of validated instruments are available"), or, for the effectiveness of acute treatment, the subject uses acute medication (OUT-023, "For each acute medication").
- Conformance: structural (a value set); a responder label SHOULD name its criterion (INV-062).
- Realises: OUT-018, OUT-020
- Evidence: Stage 1 OUT-020 (criteria named: "NICE CG150 rec. 1.3.28", "IHS global practice recommendations Q6", "IHS position statement 2025 control levels"; thresholds of NICE 1.3.28 [S-015] "at least 50% in episodic migraine" and "at least 30% in chronic migraine"; IHS Q6 [S-008] "a ≥ 50% decrease in monthly migraine days or moderate-to-severe headache days" and the PGIC and MIDAS/HIT-6 items; DMKG/ÖKSG/SKG [S-023] "mindestens 50 %", "um mindestens 5 Punkte", "um mindestens 30 %"); Stage 1 OUT-018 (NICE 1.3.29 [S-015] "at least 30% after 2 treatment cycles"; Russian section 7.1 [S-033] "на 50% и более", Caveats naming these criteria). Thresholds not quoted in Stage 1:
  - [S-008] "For patients with chronic migraine who have not achieved a ≥ 50% decrease in monthly migraine days or moderate-to-severe headache days with multiple preventive options (including oral drugs, onabotulinumtoxinA and drugs targeting the CGRP pathway), a ≥ 30% decrease in monthly migraine days or moderate-to-severe headache days is acceptable for treatment continuation beyond three months." (Q6, Recommendations, Optimal, p. 12)
  - [S-008] "The clinically meaningful improvement in MIDAS score is defined by the AHS as i) reduction of ≥5 points for baseline score 11–20 or ii) reduction of ≥30% for baseline score ≥20. The clinically meaningful improvement in HIT-6 score is a reduction of ≥ 5 points (9)." (Q6, Evidence, p. 13)
  - [S-010] the control levels quoted in E-046.
- Notes: NICE 1.3.28 words its measure "frequency of migraines"; the model applies it to migraine days, the frequency measure of OUT-018. The second clause of NICE 1.3.29 ("or if their condition has changed to episodic migraine for 3 consecutive months") is a reason to stop after success, not a response criterion, and is not modelled. The IHS Q6 MIDAS ranges overlap at a baseline score of 20, as the source states them; either component may then apply. The evaluation time point that [S-033] attaches to `critRu71` ("через 3 месяца терапии") is the rule `ruleRu71` of E-041. The scheme criteria of OUT-025 (Kela, AIFA, Poland, Zorgverzekeraars Nederland) are not responder criteria of this element; OUT-025 Caveats state that they are not requirements.

### E-046 ResponderLabel
- Definition:
```omn
element ResponderLabel extends Item {
  category : ResponderCategory  core
  treatment : Treatment  core
  evaluated : seq1 →Period  core                  -- the on-treatment period or periods the label refers to
  criterion : opt ResponderCriterion  SHOULD       -- the named criterion, shown with its thresholds
  comparison : opt →ResponseComparison  SHOULD     -- the underlying values (OUT-018)
  residual : set →ResidualBurden  SHOULD           -- the residual burden (OUT-019)
  otherValues : set →Item  SHOULD when ∃ k ∈ self.criterion • ∃ u ∈ k.alsoRestsOn • valueAvailable(ctx, u)   -- the other values the criterion rests on
}
variant ResponderCategory ::= responder | nonResponder | controlLevel ⟨ControlLevel⟩
enum ControlLevel ::= migraineFreedom | optimalControl | modestControl | insufficientControl
pred reductionMet(L : ResponderLabel, r : ReductionComponent) ≙ #L.evaluated = 1 ∧ conditionHolds(ctx(outputOf(L)), r.condition) ∧
  ∃ rc ∈ L.comparison; ch ∈ rc.changes • ch.reference.period = rc.baseline ∧ ch.compared.period ∈ ran L.evaluated ∧
    ch.reference.measure ∈ r.measures ∧ ch.reference.days > 0 ∧
    100 × (ch.reference.days − ch.compared.days) ≥ r.atLeastPercent × ch.reference.days
pred reductionDecided(L : ResponderLabel, r : ReductionComponent) ≙ ¬ conditionHolds(ctx(outputOf(L)), r.condition) ∨
  (#L.evaluated = 1 ∧ ∀ k ∈ r.measures; p ∈ ran L.evaluated • ∃ rc ∈ L.comparison; ch ∈ rc.changes •
    ch.reference.period = rc.baseline ∧ ch.reference.measure = k ∧ ch.compared.period = p ∧ ch.reference.days > 0)
pred scoreMet(L : ResponderLabel, s : ScoreComponent) ≙ conditionHolds(ctx(outputOf(L)), s.condition) ∧
  ∃ r ∈ L.otherValues ∩ InstrumentResult; b ∈ r.baselineResult; x ∈ r.totalScore; y ∈ b.totalScore •
    r.instrument = s.instrument ∧ (∀ lo ∈ s.baselineAtLeast • y ≥ lo) ∧ (∀ hi ∈ s.baselineAtMost • y ≤ hi) ∧
    ((∃ n : ℚ • s.decrease = atLeastPoints(n) ∧ y − x ≥ n) ∨
     (∃ pc : Percent • s.decrease = atLeastPercentOfBaseline(pc) ∧ y > 0 ∧ 100 × (y − x) ÷ y ≥ pc))
pred scoreDecided(L : ResponderLabel, s : ScoreComponent) ≙ ¬ conditionHolds(ctx(outputOf(L)), s.condition) ∨
  ∃ r ∈ L.otherValues ∩ InstrumentResult; b ∈ r.baselineResult • r.instrument = s.instrument ∧ r.totalScore ≠ ∅ ∧ b.totalScore ≠ ∅
pred componentMet(L : ResponderLabel, k : CriterionComponent) ≙
  (∃ r : ReductionComponent • k = reductionFromBaseline(r) ∧ reductionMet(L, r)) ∨ (∃ s : ScoreComponent • k = scoreDecrease(s) ∧ scoreMet(L, s))
pred componentDecided(L : ResponderLabel, k : CriterionComponent) ≙
  (∃ r : ReductionComponent • k = reductionFromBaseline(r) ∧ reductionDecided(L, r)) ∨ (∃ s : ScoreComponent • k = scoreDecrease(s) ∧ scoreDecided(L, s))
fun levelDays(L : ResponderLabel, p : Period) : set ℕ ≙ daysOf(viewOf(L), migraineOrModerateSevereHeadacheDays, p, allTypes)
```
- Meaning: An optional label that classifies the response to a preventive treatment under a named criterion: responder or non-responder, or a control level of the IHS position statement 2025. It is shown with the criterion it applies, the values it rests on, and the residual burden, and it is not presented as the sole indicator of individual benefit. For clinicians and patients.
- Conformance: optional: Stage 1 states no requirement to display a label ("If the output displays"), so its availability is MAY. If shown: criterion, underlying values and, where they are available, other values SHOULD (INV-062); the clinical-interpretation caveat SHOULD (INV-100). SHOULD NOT: presented as the sole indicator of individual benefit (INV-065). MUST NOT: a decision on continuing the treatment (INV-106).
- Realises: OUT-020, OUT-025, OUT-038
- Evidence: Stage 1 OUT-020. Control levels, not stated in Stage 1:
  - [S-010] "Migraine Freedom. This is defined as the complete elimination of days with migraine or moderate-to-severe headache, ideally over a period of three months." (section "Setting goals of migraine burden while on treatment", p. 6)
  - [S-010] "Optimal Control. This is defined as less than four days with migraine or moderate-to-severe headache per month for three months, with a satisfactory response to acute treatment, defined as pain-freedom within two hours from the intake." (same section, p. 6)
  - [S-010] "Modest Control. This is defined as four to six days with migraine or moderate-to-severe headache per month." (same section, p. 6)
  - [S-010] "Insufficient Control. This is defined as more than six days with migraine or moderate-to-severe headache per month." (same section, p. 6; in the PDF text layer the running header "Cephalalgia 45(2)" interrupts the sentence after "per", at a column break)
  - [S-010] "In some cases, insufficient control may be present when there are less than six MMDs, especially when attacks are associated with very high levels of disabling symptoms" (same section, p. 6)
- Notes: Relations: INV-063 (a label is consistent with the components of its criterion that can be decided from the values shown), INV-064 (control levels). A reduction of at least p % is tested on the shown monthly day counts (`100 × (reference − compared) ≥ p × reference`), not on the rounded percentage, so that rounding cannot change the result. A label may refer to several on-treatment periods (for example the three months of optimal control). For a reduction component, the cited criteria do not state how several months are combined (at a time point, on their mean, in every month, or in a share of the months). The reduction relations therefore decide only a label with a single evaluated period (`#L.evaluated = 1`). For a label over several periods, a reduction component is not decided by the values shown, as for a judgement component, and the reader applies the named criterion to the values shown with the label (INV-062). The control-level labels are exactly the four level names of [S-010]; "per month" is read as applying to each evaluated monthly period. Because [S-010] allows insufficient control with fewer than six migraine days, the model does not require more than six days for that level. A label classifies the response under a named criterion and is not a decision on continuing the treatment (INV-106). See ISS-08.

### E-047 AdherenceSummary
- Definition:
```omn
element AdherenceSummary extends Item {
  treatment : Treatment  core
  window : →Period  core                         -- the evaluation window the adherence refers to
  adherence : AdherenceValue  derived core
}
variant AdherenceValue ::= proportionOfPrescribedIntake ⟨Percent⟩ | otherAdherenceStatement ⟨Text⟩
```
- Meaning: The patient-reported adherence to the prescribed preventive regimen over the evaluation window, shown next to the response comparison, so that a reader can see whether an apparent lack of effect coincided with inconsistent intake. For clinicians and patients.
- Conformance: SHOULD next to each response comparison (INV-066); SHOULD also in the treatment history (E-055 `adherence`) and in the clinician-facing summary (INV-104).
- Realises: OUT-039
- Evidence: Stage 1 OUT-039.
- Notes: Relations: INV-067 (the window begins on or after the treatment start). Stage 1 fixes no measure of adherence. The proportion of prescribed intake is the natural numeric form; `otherAdherenceStatement` keeps the form open.

### E-048 TreatmentReviewView
- Definition:
```omn
element TreatmentReviewView extends View {
  treatment : Treatment  core
  baseline : →Period  MUST
  onTreatment : seq1 →Period  MUST
}
```
- Meaning: For treatment review, headache days, migraine days and acute-medication days (in total across classes, per ICHD-3 8.2 class and per drug, as in OUT-014) presented together for the same pre-treatment baseline and on-treatment periods, with, where provided, moderate/severe headache days, attacks, intensity, migraine-associated symptoms and the most bothersome symptom, the effectiveness of acute treatment for the attacks treated in each of these periods, and the most recent instrument and PGIC results, so that efficacy can be judged across these dimensions and against the patient's own goals. For clinicians and patients.
- Conformance: MUST be available for each preventive treatment (INV-102), with headache days, migraine days (for patients with migraine, OUT-005) and acute-medication days (the total, each ICHD-3 8.2 class of the subject's acute medications and each of their drugs) for every period (INV-068); the further components SHOULD, where provided (INV-069).
- Realises: OUT-021
- Evidence: Stage 1 OUT-021.
- Notes: The patient's own goals are what the reader brings to the view; Stage 1 does not ask the output to show them.

### E-049 PostStopMonitoringView
- Definition:
```omn
element PostStopMonitoringView extends View {
  treatment : Treatment  core
  event : CourseEventKind  core                -- stop(discontinued), stop(paused) or doseChange(reduction)
  eventDate : Date  core
  baseline : opt →Period  SHOULD               -- the original pre-treatment baseline period
  onTreatmentPeriod : opt →Period  SHOULD when ∃ s ∈ startOf(ctx, self.treatment) • s < self.eventDate   -- an on-treatment period before the event
  after : seq →Period  SHOULD                  -- consecutive periods from the event onward
}
```
- Meaning: After a preventive treatment is stopped, paused or reduced, headache and migraine frequency continue to be shown and are compared with both the on-treatment period and the original pre-treatment baseline, so that worsening or rebound above baseline is visible. For clinicians and patients.
- Conformance: SHOULD be available for each such event (INV-103); content SHOULD (INV-070). The on-treatment period SHOULD be shown whenever the event falls after the day the treatment started.
- Realises: OUT-022
- Evidence: Stage 1 OUT-022.
- Notes: "Headache and migraine frequency" is represented by headache days and migraine days; see ISS-03. An on-treatment period before the event begins on or after the treatment start and ends before the event (INV-070), so it exists only when the event is later than the start day; for a stop, pause or reduction on the start day itself, there is no such period.

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
```
- Meaning: The outcome measures of treated attacks used in the IHS acute trial guideline [S-004], FDA guidance [S-020] and the EHF definitions [S-012]: pain freedom, absence of the most bothersome symptom, headache relief and absent or minimal non-pain-symptom disturbances at the early time point (2 hours; 15 minutes for cluster headache), sustained pain freedom and maintained relief and non-pain-symptom status to 24 hours, use of rescue or repeat medication, relapse, drug-related adverse events and whether the patient regarded them as meaningful.
- Conformance: structural (a value set); used by E-051 to E-053.
- Realises: OUT-012, OUT-023, OUT-031
- Evidence: Stage 1 OUT-023, OUT-031.
- Notes: Pain freedom and headache relief are shown side by side; the output does not itself decide which definition of response applies (OUT-023 Caveats, INV-107).

### E-051 AcuteTreatmentSummary
- Definition:
```omn
element AcuteTreatmentSummary extends PeriodValue {
  drug : Drug  core
  formulationScope : FormulationScope  core
  formulations : set FormulationOrRoute  SHOULD       -- the formulations or routes of administration it summarises
  earlyTimePoint : EarlyTimePoint  core
  treatedAttacks : ℕ  derived core                    -- number of treated attacks summarised; unit: attacks
  outcomes : set →OutcomeSummary  SHOULD
  sequence : seq →TreatedAttackLine  SHOULD when self.treatedAttacks > 0   -- the treated attacks it summarises, earliest first
}
enum FormulationScope ::= allFormulations | singleFormulation
```
- Meaning: For one acute medication (all its formulations, or one formulation) and one period, the outcomes across the attacks treated with it, how consistently the drug was effective across consecutive treated attacks (the sequence of per-attack lines), and the formulation or route, so that the EHF definitions of effective attack treatment, triptan response and triptan refractoriness can be applied. Summaries for the pre-treatment baseline period and for the on-treatment periods of a preventive treatment make a change in the response to acute treatment visible. For clinicians and patients.
- Conformance: SHOULD be available per acute medication, per formulation, and separately for the baseline and on-treatment periods of each preventive treatment (INV-071); content SHOULD (INV-072), including a line for every treated attack it summarises, with the result of every outcome measure; early time point 15 minutes for cluster headache and 2 hours otherwise (INV-073). SHOULD NOT: deciding which definition of response applies (INV-107).
- Realises: OUT-012, OUT-021, OUT-023, OUT-024, OUT-031
- Evidence: Stage 1 OUT-023.
- Notes: Dose changes of acute medications are shown in the treatment history (E-055), as OUT-023 states.

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
- Conformance: SHOULD for each required outcome of the summary's time point (INV-072).
- Realises: OUT-023, OUT-031
- Evidence: Stage 1 OUT-023.
- Notes: Relations: INV-074 (`attacksWithOutcome ≤ attacksAssessed` and `attacksAssessed ≤ treatedAttacks`; `proportion ≈ 100 × attacksWithOutcome ÷ attacksAssessed`; agreement with the per-attack lines when the sequence lists all summarised attacks).

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
- Conformance: SHOULD, as the sequence of a summary, with a result for every outcome measure of the summary's early time point (INV-072); `symptomStatus` SHOULD for subjects with migraine, `hasType(ctx, c1)`, with a status for each of the three symptoms (INV-076).
- Realises: OUT-012, OUT-023
- Evidence: Stage 1 OUT-012, OUT-023.
- Notes: Relations: INV-075 (one result per measure; one status per symptom; adverse-event results agree with the adverse-event items).

### 5.7 Treatment history and scheme windows

### E-054 TreatmentHistoryView and ClassGroup
- Definition:
```omn
element TreatmentHistoryView extends View {
  preventiveGroups : seq →ClassGroup  SHOULD when ctx.subject.preventiveTreatments ≠ ∅
  acuteGroups : seq →ClassGroup  SHOULD when ctx.subject.acuteTreatments ≠ ∅
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
- Meaning: A chronological list of preventive treatments and, separately, of acute treatments, grouped by drug class. For clinicians (primary) and patients. The list shows the treatments that were tried; it does not show drugs that could not be used, nor debilitating days, so it supports but does not by itself establish eligibility for later treatments or for the EHF categories of resistant and refractory migraine (OUT-024 Caveats).
- Conformance: SHOULD be available (INV-077); grouping and order SHOULD (INV-078).
- Realises: OUT-024, OUT-039
- Evidence: Stage 1 OUT-024.
- Notes: `DrugClass` is a given set because Stage 1 names no class system for preventive drugs.

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
  preventiveResponse : opt →ResponseComparison  SHOULD when self.role = preventive ∧ startOf(ctx, self.treatment) ≠ ∅
  acuteResponse : set →AcuteTreatmentSummary  SHOULD when self.role = acute
  adverseEffects : opt AdverseEffects  SHOULD
  stopReason : opt StopReason  SHOULD when stopped(ctx, self.treatment)
  formulations : set FormulationOrRoute  SHOULD when self.role = acute
  adherence : opt →AdherenceSummary  SHOULD when self.role = preventive ∧ startOf(ctx, self.treatment) ≠ ∅
}
value DoseChangeItem { date : Date; direction : DoseChangeDirection; newDose : opt Text }
variant AdverseEffects ::= noAdverseEffects | adverseEffectsShown ⟨set1 Text⟩
variant StopReason ::= lackOfEfficacy | adverseEffectsReason | otherStopReason ⟨Text⟩
pred stopped(c : OutputContext, t : Treatment) ≙ ∃ e ∈ c.subject.courseEvents • e.treatment = t ∧ e.kind is stop
pred hasDoseChange(c : OutputContext, t : Treatment) ≙ ∃ e ∈ c.subject.courseEvents • e.treatment = t ∧ e.kind is doseChange
```
- Meaning: One treatment of the history: start and stop dates, dose changes, treatment duration (from the start to the stop or, for a treatment that has not stopped, to the as-of date of the output, that is, its duration to date), the response summary (from OUT-018 for preventive and OUT-023 for acute treatments), adverse effects during the treatment, the reason for stopping, for acute treatments the formulation, and for preventive treatments the adherence (OUT-039).
- Conformance: SHOULD (INV-077), each attribute as declared. The start date, the duration, and for a preventive treatment the response comparison and the adherence SHOULD be shown whenever the treatment has a start; the stop date and the stop reason whenever it has stopped.
- Realises: OUT-024, OUT-039
- Evidence: Stage 1 OUT-024, OUT-039.
- Notes: Relations: INV-079 (stop not before start; duration agrees with the start and the stop date, or with the start and the as-of date for a treatment that has not stopped; dates and dose changes agree with the subject's course events). The `when` clauses state when the content can exist: a start date, a duration and a response comparison aligned to the start (INV-056) exist only for a treatment that has a start, and adherence refers to the time on treatment (INV-067). Every course event lies on or before the as-of date (INV-001), so whether a treatment has stopped is judged as of that date, and the duration of a treatment that has not stopped runs to it; the period the history view covers need not contain the treatment's start, because the history lists every treatment (INV-077). The stop reasons name the failure modes of the OUT-024 rationale (lack of efficacy, adverse effects); `otherStopReason` keeps the list open.

### E-056 SchemeWindowView
- Definition:
```omn
element SchemeWindowView extends View {
  scheme : SchemeName  core                     -- shown as the label of the view
  windows : seq1 →Period  core                  -- the evaluation windows the clinician selected
}
```
- Meaning: Frequency, disability and treatment-history outputs for evaluation windows defined by a national reimbursement or monitoring scheme (for example specified treatment weeks, the three months preceding an application, month-by-month responder views or six-monthly reassessments), labelled with the name of the scheme. For clinicians preparing reimbursement or registry documentation.
- Conformance: MAY, for contexts with a scheme selection (`ctx.schemeSelection ≠ ∅`). Its content (headache days and migraine days per window, instrument results, treatment lines, responder labels) is MAY.
- Realises: OUT-025
- Evidence: Stage 1 OUT-025.
- Notes: Relations: INV-080 (the windows are the selected windows, and the label is the selected scheme). Scheme criteria are not shown as requirements of the model (OUT-025 Caveats).

### 5.8 Instruments

### E-057 Instrument value sets
- Definition:
```omn
enum Instrument ::= midas | hit6 | msq21 | halt90 | halt30 | hurt | mtoq | pedmidas | pgic
fun instrumentName : Instrument → Text
axiom instrumentName(midas) = "MIDAS" ∧ instrumentName(hit6) = "HIT-6" ∧ instrumentName(msq21) = "MSQ v2.1" ∧
  instrumentName(halt90) = "HALT-90" ∧ instrumentName(halt30) = "HALT-30" ∧ instrumentName(hurt) = "HURT" ∧
  instrumentName(mtoq) = "M-TOQ" ∧ instrumentName(pedmidas) = "PedMIDAS" ∧ instrumentName(pgic) = "PGIC"
variant RecallPeriod ::= recallMonths ⟨ℕ₁⟩ | recallAsPublished ⟨Text⟩
fun publishedRecall : Instrument ⇸ RecallPeriod      -- defined for midas, hit6, pedmidas, halt90, halt30
axiom publishedRecall(midas) = recallMonths(3) ∧ publishedRecall(hit6) = recallMonths(1) ∧
  publishedRecall(pedmidas) = recallMonths(3) ∧ publishedRecall(halt90) = recallMonths(3) ∧ publishedRecall(halt30) = recallMonths(1)
value ScoreRange { low : ℚ; high : opt ℚ }            -- inclusive bounds; high = ∅: the model states no upper bound
fun scoreRange : Instrument ⇸ ScoreRange             -- defined for hit6, midas, pedmidas, halt90, halt30
axiom scoreRange(hit6) = ScoreRange(low ↦ 36, high ↦ {78}) ∧ scoreRange(midas) = ScoreRange(low ↦ 0, high ↦ ∅) ∧
  scoreRange(pedmidas) = ScoreRange(low ↦ 0, high ↦ ∅) ∧ scoreRange(halt90) = ScoreRange(low ↦ 0, high ↦ ∅) ∧
  scoreRange(halt30) = ScoreRange(low ↦ 0, high ↦ ∅)
const wholeNumberScores : set Instrument ≙ {midas, hit6, pedmidas, halt90, halt30}   -- instruments whose total score is a whole number
value GradeBand { instrument : Instrument; grade : opt Text; label : Text; low : ℚ; strictLow : 𝔹; high : opt ℚ }
pred inBand(x : ℚ, b : GradeBand) ≙ (b.strictLow ⇒ x > b.low) ∧ (¬ b.strictLow ⇒ x ≥ b.low) ∧ ∀ h ∈ b.high • x ≤ h
const gradeBands : set1 GradeBand ≙ {
  GradeBand(instrument ↦ midas, grade ↦ {"I"}, label ↦ "little or no disability", low ↦ 0, strictLow ↦ false, high ↦ {5}),
  GradeBand(instrument ↦ midas, grade ↦ {"II"}, label ↦ "mild disability", low ↦ 6, strictLow ↦ false, high ↦ {10}),
  GradeBand(instrument ↦ midas, grade ↦ {"III"}, label ↦ "moderate disability", low ↦ 11, strictLow ↦ false, high ↦ {20}),
  GradeBand(instrument ↦ midas, grade ↦ {"IV"}, label ↦ "severe disability", low ↦ 21, strictLow ↦ false, high ↦ ∅),
  GradeBand(instrument ↦ hit6, grade ↦ ∅, label ↦ "little or no impact", low ↦ 36, strictLow ↦ false, high ↦ {49}),
  GradeBand(instrument ↦ hit6, grade ↦ ∅, label ↦ "some impact", low ↦ 50, strictLow ↦ false, high ↦ {55}),
  GradeBand(instrument ↦ hit6, grade ↦ ∅, label ↦ "substantial impact", low ↦ 56, strictLow ↦ false, high ↦ {59}),
  GradeBand(instrument ↦ hit6, grade ↦ ∅, label ↦ "severe impact", low ↦ 60, strictLow ↦ false, high ↦ {78}),
  GradeBand(instrument ↦ pedmidas, grade ↦ ∅, label ↦ "Little to none", low ↦ 0, strictLow ↦ false, high ↦ {10}),
  GradeBand(instrument ↦ pedmidas, grade ↦ ∅, label ↦ "Mild", low ↦ 11, strictLow ↦ false, high ↦ {30}),
  GradeBand(instrument ↦ pedmidas, grade ↦ ∅, label ↦ "Moderate", low ↦ 31, strictLow ↦ false, high ↦ {50}),
  GradeBand(instrument ↦ pedmidas, grade ↦ ∅, label ↦ "Severe", low ↦ 50, strictLow ↦ true, high ↦ ∅),
  GradeBand(instrument ↦ halt90, grade ↦ {"I"}, label ↦ "Minimal or infrequent", low ↦ 0, strictLow ↦ false, high ↦ {5}),
  GradeBand(instrument ↦ halt90, grade ↦ {"II"}, label ↦ "Mild or infrequent", low ↦ 6, strictLow ↦ false, high ↦ {10}),
  GradeBand(instrument ↦ halt90, grade ↦ {"III"}, label ↦ "Moderate", low ↦ 11, strictLow ↦ false, high ↦ {20}),
  GradeBand(instrument ↦ halt90, grade ↦ {"IV"}, label ↦ "Severe", low ↦ 20, strictLow ↦ false, high ↦ ∅) }
fun publishedGrading : Instrument → 𝔹                -- the instrument's developer publishes a grading or categories
axiom publishedGrading(midas) ∧ publishedGrading(hit6) ∧ publishedGrading(pedmidas) ∧ publishedGrading(halt90) ∧
  publishedGrading(hurt) ∧ publishedGrading(pgic) ∧ ¬ publishedGrading(halt30)
fun banded : Instrument → 𝔹                          -- the model tabulates grade bands for the instrument
axiom ∀ i : Instrument • banded(i) ⇔ (∃ b ∈ gradeBands • b.instrument = i)
```
- Meaning: The instruments named in Stage 1 OUT-026 (MIDAS, HIT-6, MSQ v2.1, HALT, HURT, the Migraine Treatment Optimization Questionnaire, PedMIDAS for children, PGIC) with the parts of their published value sets that the model states: the instrument name as shown, the recall period, the score range, and the grade or category labels with their score bands, exactly as the cited source words them. For instruments whose value sets the model does not tabulate (MSQ v2.1, HURT, M-TOQ, PGIC), results show the instrument's own published scores and categories by name (`recallAsPublished`, `publishedCategory`).
- Conformance: structural (value sets).
- Realises: OUT-026, OUT-036
- Evidence: Stage 1 OUT-026 (recall periods of HIT-6 "1-month recall period" and MIDAS "3-month recall period" [S-002]; HURT "no concern" and three flagged areas, and "Grading is not used by HALT-30" [S-014]), OUT-036 (PedMIDAS "over the previous 3 months" [S-005]). Details not stated in Stage 1:
  - [S-101] "[...] ranges between 36 and 78, with larger scores reflecting greater impact" (Methods, "Data sources", HIT-6 paragraph; the omitted words describe how the score is obtained)
  - [S-101] "The four headache impact severity categories are little or no impact (49 or less), some impact (50–55), substantial impact (56–59), and severe impact (60–78)." (Methods, "Data sources", HIT-6 paragraph)
  - [S-102] "[...] four grades based on total days of impaired functioning (i.e., Grade I or little or no disability, 0 to 5; Grade II or mild disability, 6 to 10; Grade III or moderate disability, 11 to 20; Grade IV or severe disability, ≥21, with an option of dividing Grade IV into IVA and IVB)." (Methods, "Headache impact on functioning", subsection "Migraine-related disability")
  - [S-102] "The recall period for the MIDAS is three months" (same subsection, the sentence after the grades)
  - [S-103] "The PedMIDAS grading scale is as follows:" followed by the table rows "0 to 10" "Little to none", "11 to 30" "Mild", "31 to 50" "Moderate" and "Greater than 50" "Severe" under the headings "PedMIDAS Score Range" and "Disability Grade" (section "PedMIDAS Grading Scale")
  - [S-014] "HALT-90 (Fig. 3 (also, Additional file 18 )) counts days affected by headache during the preceding 3 months (90 days)." (section "The Headache-Attributed Lost Time (HALT) Indices", paragraph beginning "There are three versions of HALT"; quoted from the Europe PMC full text, where figure references are rendered with spaces)
  - [S-014] "HALT-30 (Fig. 4 (also, Additional file 19 )) accordingly records days affected during the preceding 1 month (30 days)." (same paragraph)
  - [S-014] "the unit of each being whole days per one or 3 months" (subsection "Scoring HALT", first sentence)
  - [S-014] Table 18 "Grading of HALT-90", columns "Days lost in last 3 months", "Assessed impact" and "Grade (indicating increasing need for medical care)", rows "0–5" "Minimal or infrequent" "I", "6–10" "Mild or infrequent" "II", "11–20" "Moderate" "III (indicates high need for care)" and "≥20" "Severe" "IV (indicates high need for care)" (subsection "Scoring HALT")
  - Whole-number scores (`wholeNumberScores`), from the quotes above: the MIDAS grades rest on "total days of impaired functioning" [S-102], and the HALT unit is "whole days per one or 3 months" [S-014]; the published bands of MIDAS [S-102], HIT-6 [S-101], PedMIDAS [S-103] and HALT-90 [S-014] have consecutive whole-number limits (for example 0 to 5 and 6 to 10 for MIDAS, 49 or less and 50–55 for HIT-6, 0 to 10 and 11 to 30 for PedMIDAS), so the categories that these sources define over the score range cover it only for whole-number scores.
- Notes: Relations: INV-082. MIDAS grade labels differ between publications of the MIDAS developers (for example "minimal or infrequent disability" in other papers); the model uses the labels of [S-102] and the same score bands. The HALT-90 bands of [S-014] overlap at 20 ("11–20" and "≥20"), as also printed in the HALT developers' 2018 paper; at a score of 20 either grade III or IV satisfies the relation. The lower bound 0 of MIDAS, PedMIDAS and HALT follows from their lowest band. The cited sources state no upper bound for these instruments, so the model states none: `high = ∅` means that the model states no upper bound, not that the score range has none. The total scores of MIDAS, PedMIDAS, HALT-90, HALT-30 and HIT-6 are whole numbers (`wholeNumberScores`, INV-082); source sentences that describe how a total is obtained from the answers are not quoted, because that derivation is out of scope. HURT grades each response into an area of "no concern" or one of three flagged areas [S-014]; see ISS-06. The scoring of every instrument from its answers is out of scope. `publishedGrading` is not fixed by the model for MSQ v2.1 and M-TOQ; it follows those instruments' own publications, which the model does not tabulate.

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
- Meaning: The result of one administration of a validated impact, disability or quality-of-life instrument: name, completion date, recall period, total score, the instrument's own published grading or categories, and the change from the baseline administration. For clinicians, patients and researchers.
- Conformance: SHOULD, where results are available (INV-081). For children, PedMIDAS results with their 3-month recall period SHOULD (INV-096). The baseline result and the change from it SHOULD be shown whenever an earlier result of the same instrument is available.
- Realises: OUT-020, OUT-021, OUT-025, OUT-026, OUT-034, OUT-036
- Evidence: Stage 1 OUT-026, OUT-036.
- Notes: Relations: INV-082 (score in range; category is the band containing the score; recall is the published recall; the baseline administration is an earlier available result of the same instrument; change = score − baseline score). A first administration has no earlier result, so `baselineResult` is required only when an earlier result exists, as in INV-081. The output reports results and their change; it does not make MIDAS or HIT-6 a criterion of efficacy (OUT-026 Caveats), except where a named responder criterion that the reader applies uses them (E-045). See ISS-06.

### E-059 ScreeningResult
- Definition:
```omn
element ScreeningResult extends Item {
  instrument : ScreeningInstrument  core
  date : opt Date  SHOULD
  scores : set SubscaleScore  SHOULD
}
variant ScreeningInstrument ::= hads | phq9 | gad7 | otherScreeningInstrument ⟨Text⟩
value SubscaleScore { subscale : Subscale; score : ℕ }     -- unit: score points
enum Subscale ::= wholeScale | anxietySubscale | depressionSubscale
fun screeningName : ScreeningInstrument → Text
axiom screeningName(hads) = "HADS" ∧ screeningName(phq9) = "PHQ-9" ∧ screeningName(gad7) = "GAD-7" ∧
  ∀ x : Text • screeningName(otherScreeningInstrument(x)) = x
```
- Meaning: The result of a depression or anxiety screening instrument (for example HADS, PHQ-9, GAD-7): instrument name, date and score, shown next to the headache outputs as a screening result, not as a psychiatric diagnosis. For clinicians.
- Conformance: SHOULD, where results are available, next to headache outputs (INV-083). SHOULD NOT: presented as a psychiatric diagnosis (INV-084).
- Realises: OUT-033, OUT-038
- Evidence: Stage 1 OUT-033. Score ranges, not stated in Stage 1:
  - [S-104] "[...] the possible scores ranged from 0 to 21 for anxiety and 0 to 21 for depression." (section "Construction of the Hospital Anxiety And Depression Scale (HADS)"; the omitted words describe how the scores are obtained)
  - [S-105] "PHQ-9 total score for the nine items ranges from 0 to 27." (section "Use of some screeners as severity and outcome measures", P. 6/9)
  - [S-105] "GAD-7 total score for the seven items ranges from 0 to 21." (same section, P. 6/9)
- Notes: Relations: INV-085. Stage 1 asks for the score only; severity categories of these instruments are not part of the output and are not stated.

### 5.9 Special populations and classification support

### E-060 MenstrualRelationView and CycleLine
- Definition:
```omn
element MenstrualRelationView extends View {
  cycles : seq1 →CycleLine  core               -- consecutive menstrual cycles, earliest first
  completeCycles : ℕ  derived MUST             -- the number of complete cycles the view covers
}
element CycleLine extends Item {
  cycle : DateSpan  core                        -- from the first day of menstruation to the day before the next one; for a cycle
                                                --   that has not ended, to the last day of the period the view covers
  complete : 𝔹  core                            -- the cycle has ended: it is shown to the day before the next first day of menstruation
  menstruationDays : set1 Date  MUST
  firstDayOfMenstruation : Date  derived MUST   -- day 1
  perimenstrualWindow : DateSpan  derived MUST  -- ICHD-3 appendix A1.1: day 1 ± 2 (days −2 to +3)
  migraineDays : set Date  MUST                 -- the migraine days of the cycle
  attacks : set →AttackMark  MUST               -- the migraine attacks of the cycle
}
const windowDaysBefore : ℕ ≙ 2                  -- day −2 is 2 days before day 1
const windowDaysAfter : ℕ ≙ 2                   -- day +3 is 2 days after day 1, because there is no day 0
```
- Meaning: For patients who menstruate, migraine attacks and migraine days in relation to the days of menstruation across consecutive cycles, with the perimenstrual window of ICHD-3 appendix A1.1 distinguished from the other days of the cycle, and the number of complete cycles the view covers. For clinicians and patients.
- Conformance: MUST be available for subjects who menstruate (INV-086); `completeCycles` MUST.
- Realises: OUT-030, OUT-035
- Evidence: Stage 1 OUT-030. The window, not stated in Stage 1:
  - [S-001] "Occurring exclusively on day 1 ± 2 (i.e. days −2 to +3)" (A1.1.1 Pure menstrual migraine without aura, diagnostic criterion B, p. 190; the "±" and "−" signs are glyphs without a text mapping in the PDF text layer); the same window appears in A1.1.2 criterion B ("Occurring on day 1 ± 2 (i.e. days −2 to +3)", p. 190)
  - [S-001] "The first day of menstruation is day 1 and the preceding day is day −1; there is no day 0." (A1.1.1, note 2, p. 190; the text layer breaks "preceding" at a line end)
- Notes: Relations: INV-087. For every cycle line, in whichever view it is shown (here, or in the patient-facing overview, INV-105): day 1 is the first menstruation day; the window runs from 2 days before to 2 days after day 1; a cycle that has not ended is shown to the end of the period its view covers; its attacks are shown in the same view and lie in the cycle; an attack is marked as in the window exactly when its onset is a window day of a cycle shown in the same view. In this view: cycles are consecutive, overlap the covered period and are shown in the view; only the last cycle can be one that has not ended; `completeCycles` is the number of cycles that have ended and lie wholly within the period the view covers. Reading "complete cycles the view covers" as cycles that have ended and lie wholly within the covered period is the model's; a cycle that began before the covered period, or ends after it, is shown but not counted. Only the window of the criterion is shown; the frequency criterion ("in at least two out of three menstrual cycles") is a diagnostic criterion and is not applied by the view. A prospective diary is not mandatory for the clinical diagnosis of A1.1.1 and A1.1.2 (OUT-030 Caveats); the view states no diagnosis.

### E-061 AttackMark
- Definition:
```omn
element AttackMark extends Item {
  onset : Date  core
  inPerimenstrualWindow : 𝔹  derived MUST
}
```
- Meaning: A migraine attack shown in the menstrual-relation view by its onset date, marked as inside or outside the perimenstrual window.
- Conformance: MUST within E-060.
- Realises: OUT-030
- Evidence: Stage 1 OUT-030.
- Notes: Relations: INV-087 (the mark shows the attack as in the window exactly when its onset falls in the perimenstrual window of a cycle shown in the same view; this holds in every view in which an attack mark is shown).

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
- Meaning: For patients with cluster headache: cluster periods (bouts) and cluster remission periods with start dates, end dates and durations, using the ICHD-3 definitions; attacks per day and per week during active periods; the effectiveness of acute treatments at 15 minutes and the need for rescue treatment; and the history of previous bouts. For clinicians and patients.
- Conformance: SHOULD be available for subjects with cluster headache, `hasType(ctx, c3_1)` (INV-088). `acute` SHOULD where the subject uses acute medication (OUT-031: "for acute treatments").
- Realises: OUT-031
- Evidence: Stage 1 OUT-031.
- Notes: Attack frequency may decrease at the end of a bout, so such changes are not treatment effects (OUT-031 Caveats); the model adds no annotation for this because Stage 1 does not ask the output to state it.

### E-063 ClusterPeriodItem and RemissionPeriodItem
- Definition:
```omn
abstract element ClusterPhaseItem extends Item {
  start : opt Date  SHOULD
  end : opt Date  SHOULD when ¬ self.ongoing
  ongoing : 𝔹  core                                -- the period continues at the end of the period the view covers
  duration : opt Duration  derived SHOULD
}
element ClusterPeriodItem extends ClusterPhaseItem { }
element RemissionPeriodItem extends ClusterPhaseItem { }
const remissionMoreThanMonths : ℕ₁ ≙ 3
fun lastDay(x : ClusterPhaseItem) : set Date ≙
  {d : Date | (x.ongoing ∧ d = viewOf(x).covers.end) ∨ (¬ x.ongoing ∧ d ∈ x.end)}   -- the end date, or the end of the covered period while ongoing
```
- Meaning: A cluster period ("the time during which cluster headache attacks occur regularly and at least once every other day", ICHD-3 Definitions of terms) or a cluster remission period (an attack-free period that ICHD-3 considers a remission), shown with its start date, end date and duration. An ongoing period has no end date yet.
- Conformance: SHOULD within E-062.
- Realises: OUT-031
- Evidence: Stage 1 OUT-031 (definitions quoted from [S-001]). Not stated in Stage 1:
  - [S-001] "To be considered a remission, the attack-free period must exceed three months." (Definitions of terms, Cluster remission period, p. 209)
- Notes: Relations: INV-089 (duration agrees with the dates; a remission period shown lasts more than three months; periods are in order and do not overlap). The output shows start, end and duration of each attack-free period but not the ICHD-3 element "cannot be induced with alcohol or nitroglycerine" (OUT-031 Caveats). `ongoing` is needed so that the end-date obligation can be met for a current bout.

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
- Meaning: The number of cluster headache attacks per day or per week during an active period (bout).
- Conformance: SHOULD within E-062, both per day and per week (INV-088).
- Realises: OUT-031
- Evidence: Stage 1 OUT-031.
- Notes: Relations: INV-089 (the rate's period lies within its bout; the rate is not negative).

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
- Meaning: The co-occurrence over time of attacks with a potential trigger factor, with the statements that it shows co-occurrence and not causation and that some apparent triggers are early (premonitory) symptoms of the attack. For patients and clinicians.
- Conformance: MAY; when shown, the two caveats SHOULD (INV-090) and the clinical-interpretation caveat SHOULD (INV-100).
- Realises: OUT-032, OUT-038
- Evidence: Stage 1 OUT-032.

### 5.10 Audience-specific views

### E-066 ClinicianSummary
- Definition:
```omn
element ClinicianSummary extends View { }
```
- Meaning: A concise clinician-facing summary for the period since the previous consultation, or a period chosen by the clinician, that brings together the outputs most used in consultations: frequency measures and their time course (OUT-004 to OUT-009), acute-medication use and any medication-overuse indicator (OUT-014 to OUT-016), current and past treatments with response (OUT-018, OUT-023, OUT-024), instrument results (OUT-026), functional impact (OUT-027), completeness (OUT-003) and adherence (OUT-039). It can be shared with the treating clinician. For primary-care clinicians, neurologists and headache specialists.
- Conformance: SHOULD be available for clinician audiences, for the selected period and for the period since the previous consultation (INV-094); content SHOULD (INV-104).
- Realises: OUT-034, OUT-039
- Evidence: Stage 1 OUT-034, OUT-039.
- Notes: "Shareable with the treating clinician" is represented by availability for contexts whose audience is a clinician; the means of sharing is delivery and out of scope. See ISS-04 on OUT-008 within "OUT-004 to OUT-009".

### E-067 PatientOverview
- Definition:
```omn
element PatientOverview extends View { }
```
- Meaning: An understandable overview, in plain language, of the patient's own headache pattern over time: headache and migraine days, intensity, acute-medication use, treatment effect and, where relevant, the relationship to menstruation, so that patients can follow the effect of their treatment and prepare consultations. For patients, parents and caregivers.
- Conformance: SHOULD be available for patient, parent and caregiver audiences (INV-095); content SHOULD (INV-105).
- Realises: OUT-035
- Evidence: Stage 1 OUT-035.
- Notes: Migraine days are included as OUT-035 states them; see ISS-03. The relationship to menstruation is shown by cycle lines (E-060) that overlap the covered period; INV-087 defines them in this view as in the menstrual-relation view.

## 6. Invariants

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
(∀ d ∈ c.previousConsultation • d ≤ c.asOf) ∧
c.subject.preventiveTreatments ∩ c.subject.acuteTreatments = ∅ ∧
(∀ p ∈ c.subject.preventiveTypes • p.1 ∈ c.subject.preventiveTreatments) ∧
(∀ t ∈ c.subject.preventiveTreatments • ∃ ty : PreventiveTreatmentType • (t, ty) ∈ c.subject.preventiveTypes) ∧
(∀ e ∈ c.subject.courseEvents • e.treatment ∈ c.subject.preventiveTreatments ∪ c.subject.acuteTreatments ∧ e.date ≤ c.asOf) ∧
(∀ t ∈ c.subject.preventiveTreatments ∪ c.subject.acuteTreatments • #{e ∈ c.subject.courseEvents | e.treatment = t ∧ e.kind = start} ≤ 1) ∧
(∀ e ∈ c.subject.courseEvents; s ∈ startOf(c, e.treatment) • s ≤ e.date) ∧
(∀ m ∈ c.subject.acuteMedications • m.drug ∈ dom classOf) ∧
(∀ d ∈ c.subject.withdrawalStart • d ≤ c.asOf) ∧
(∀ a ∈ c.subject.instrumentAdministrations • a.date ≤ c.asOf) ∧ (∀ a ∈ c.subject.screeningAdministrations • a.date ≤ c.asOf)
```
- Reading: The headache types the subject has are among those the subject has or may have, and no listed type is a subtype of another; tension-type and cluster headache make weekly granularity clinically relevant; the selected time range ends no later than the as-of date and consists of whole periods of the selected granularity; selected comparison periods, the previous consultation, treatment course events, the start of withdrawal and the available instrument results lie on or before the as-of date; a treatment is either preventive or acute and has at most one start, and none of its other course events (dose changes, the date the target or tolerated dose was reached, the end of a treatment cycle, a stop or pause) precedes its start; every preventive treatment has at least one guidance type (`otherPreventive` when no other type describes it), so that the guidance time points for all preventive types apply to it; every acute medication belongs to an ICHD-3 8.2 class.
- Conformance: definitional (characterises `Ctx`, section 3.2). Scope: context.
- Realises: OUT-001, OUT-004, OUT-009, OUT-014, OUT-018, OUT-024, OUT-029
- Evidence: Stage 1 OUT-001, OUT-004, OUT-009 ("where weekly granularity is clinically relevant (tension-type headache, cluster headache, early onset of effect)"), OUT-014, OUT-018 ("For each preventive treatment [...] at the evaluation time points named in current guidance, which differ by treatment type"; periods "after treatment start, aligned to the treatment start date"), OUT-024 ("start and stop dates"), OUT-029.
- Notes: The order of course events is part of what a treatment's start is: the course of a treatment begins with it. It ensures that a stop date shown in the treatment history is not before the start date (INV-079), and that the anchor of every evaluation rule lies on or after the start (E-041 Notes).

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
∀ v : View • v.covers ∈ v.content ∧ refs(v) ∩ Period ⊆ v.content ∧ ∀ x ∈ v.content • refs(x) ∩ Period ⊆ v.content
```
- Reading: The reporting period a view covers is shown in the view, and every period that the view or one of its items refers to (the period of a measure, the periods of a series or a comparison, a window or span) is shown, with its dates and length, in the same view.
- Conformance: MUST. Scope: output.
- Realises: OUT-001
- Evidence: Stage 1 OUT-001 ("Every summary output MUST state the reporting period it covers (start date, end date and length)").

### INV-004 A series consists of consecutive periods of its granularity
- Predicate:
```omn
∀ sr : Series • consecutive(sr.periods) ∧ ∀ p ∈ ran sr.periods • p.kind = sr.granularity
```
- Reading: Each period of a series begins on the day after the previous one ends, and all periods have the series granularity.
- Conformance: definitional (E-006). Scope: output.
- Realises: OUT-001, OUT-004, OUT-009
- Evidence: Stage 1 OUT-004 ("shown for every period in the selected time range"), OUT-009 ("a time series of consecutive reporting periods").

### INV-005 A number of days does not exceed the period length
- Predicate:
```omn
∀ m : DayCount • m.days ≤ m.period.lengthDays
```
- Reading: A number of days within a period is at most the length of that period in days.
- Conformance: definitional (E-014). Scope: output.
- Realises: OUT-001, OUT-004, OUT-005, OUT-006, OUT-008, OUT-014, OUT-015, OUT-027
- Evidence: Stage 1 statements of the requirements listed.

### INV-006 One value per measure, period and scope in a view
- Predicate:
```omn
(∀ v : View • ∀ m, n ∈ v.content ∩ DayCount • m.measure = n.measure ∧ m.period = n.period ∧ m.typeScope = n.typeScope ⇒ m = n) ∧
(∀ v : View • ∀ m, n ∈ v.content ∩ EventCount • m.event = n.event ∧ m.period = n.period ∧ m.typeScope = n.typeScope ⇒ m = n)
```
- Reading: A view does not show two different values of the same count for the same period and type scope.
- Conformance: definitional (E-014, E-019). Scope: output.
- Realises: OUT-004, OUT-007
- Evidence: Stage 1 OUT-004, OUT-007.

### INV-007 An annotation is shown with what it qualifies
- Predicate:
```omn
∀ a : Annotation • ∀ e ∈ a.qualifies • e = viewOf(a) ∨ e ∈ viewOf(a).content
```
- Reading: A label or caveat qualifies its own view or items of its own view, so it is shown together with them.
- Conformance: definitional (E-010). Scope: output.
- Realises: OUT-011, OUT-016, OUT-017, OUT-032, OUT-037, OUT-038
- Evidence: Stage 1 statements of the requirements listed.

### 6.2 Definition labels and completeness

### INV-008 Definition labels for the defined measures
- Predicate:
```omn
∀ v : View; lm : LabelledMeasure • (∃ m ∈ v.content ∩ PeriodValue • isMeasure(m, lm)) ⇒
  ∃ l ∈ v.content ∩ DefinitionLabel • l.measure = lm
```
- Reading: A view that shows migraine days, headache days, moderate/severe headache days or attacks states which published definition of each it follows.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-002, OUT-005, OUT-006, OUT-007, OUT-028
- Evidence: Stage 1 OUT-002, OUT-005 (label SHOULD), OUT-006 ("with the definition named as in OUT-002"), OUT-007, OUT-028.

### INV-009 Headache days follow ICHD-3
- Predicate:
```omn
∀ l : DefinitionLabel • l.measure = headacheDaysMeasure ⇒ l.definition = ichd3HeadacheDays
```
- Reading: The definition stated for headache days is that of ICHD-3 "Definitions of terms".
- Conformance: MUST. Scope: output.
- Realises: OUT-004
- Evidence: Stage 1 OUT-004 ("with 'headache days' as defined in ICHD-3 'Definitions of terms'").

### INV-010 Attacks follow ICHD-3
- Predicate:
```omn
∀ l : DefinitionLabel • l.measure = attacksMeasure ⇒ l.definition = ichd3FrequencyOfAttacks
```
- Reading: The definition stated for the number of attacks is "frequency of attacks" of ICHD-3 "Definitions of terms".
- Conformance: SHOULD. Scope: output.
- Realises: OUT-007
- Evidence: Stage 1 OUT-007.

### INV-011 A completeness indicator accompanies each reporting period
- Predicate:
```omn
∀ v : View • ∀ m ∈ v.content ∩ PeriodValue • m ∉ CompletenessIndicator ⇒
  ∃ ci ∈ v.content ∩ CompletenessIndicator • ci.period = m.period
```
- Reading: For every reporting period for which a view shows a summary measure, the same view shows how completely the period is covered by diary information, as a number of covered days, a proportion, or both.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-003, OUT-034
- Evidence: Stage 1 OUT-003 ("shown next to the summary measures"), OUT-034 (completeness in the clinician-facing summary).

### INV-012 Completeness values agree with the period
- Predicate:
```omn
∀ ci : CompletenessIndicator • ci.typeScope = allTypes ∧
  (∀ e₁, e₂ ∈ ci.expressions • (e₁ is coveredDays ∧ e₂ is coveredDays) ∨ (e₁ is proportionCovered ∧ e₂ is proportionCovered) ⇒ e₁ = e₂) ∧
  (∀ n : ℕ • coveredDays(n) ∈ ci.expressions ⇒ n ≤ ci.period.lengthDays) ∧
  (∀ n : ℕ; q : Percent • coveredDays(n) ∈ ci.expressions ∧ proportionCovered(q) ∈ ci.expressions ⇒ q ≈ 100 × n ÷ ci.period.lengthDays)
```
- Reading: Completeness refers to the whole period and is expressed at most once in each form; the covered days do not exceed the period length; a proportion shown with the covered days is the covered days divided by the period length, in per cent.
- Conformance: definitional (E-013). Scope: output.
- Realises: OUT-003
- Evidence: Stage 1 OUT-003 ("expressed as the proportion of days of the period that the diary covers").

### INV-013 No completeness cut-off presented as clinically validated
- Predicate:
```omn
¬ ∃ x : Element • clinicallyValidatedCutoff ∈ x.claims
```
- Reading: No element presents a fixed completeness cut-off as clinically validated.
- Conformance: SHOULD NOT. Scope: output.
- Realises: OUT-003
- Evidence: Stage 1 OUT-003 and its Caveats.

### 6.3 Frequency, severity and other per-period values

### INV-014 Headache days per reporting period
- Predicate:
```omn
∃ g ∈ MonthlyKind • ∀ c ∈ Ctx • c.granularity = g ⇒ reportedPerPeriod(c, HeadacheDays, allTypes)
```
- Reading: For calendar months or for 28-day periods (at least one of the two), every output context can be answered with headache days for every period of the selected time range.
- Conformance: MUST. Scope: repertoire.
- Realises: OUT-001, OUT-004
- Evidence: Stage 1 OUT-001 ("Frequency outputs MUST be available per calendar month or per 28-day (4-week) period"), OUT-004.

### INV-015 Migraine days per reporting period, for patients with migraine
- Predicate:
```omn
∃ g ∈ MonthlyKind • ∀ c ∈ Ctx • c.granularity = g ∧ hasType(c, c1) ⇒ reportedPerPeriod(c, MigraineDays, allTypes)
```
- Reading: For patients with migraine, migraine days are available for every period of the selected time range, per calendar month or per 28-day period.
- Conformance: MUST. Scope: repertoire.
- Realises: OUT-001, OUT-005
- Evidence: Stage 1 OUT-001, OUT-005.

### INV-016 Moderate/severe headache days per reporting period
- Predicate:
```omn
∃ g ∈ MonthlyKind • ∀ c ∈ Ctx • c.granularity = g ⇒ reportedPerPeriod(c, ModerateSevereHeadacheDays, allTypes)
```
- Reading: Days with headache of moderate or severe intensity are available per reporting period.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-001, OUT-006
- Evidence: Stage 1 OUT-001, OUT-006.

### INV-017 Attacks per reporting period
- Predicate:
```omn
∃ g ∈ MonthlyKind • ∀ c ∈ Ctx • c.granularity = g ⇒ reportedPerPeriod(c, AttackCount, allTypes)
```
- Reading: The number of attacks is available per reporting period, as a value of its own.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-001, OUT-007
- Evidence: Stage 1 OUT-001, OUT-007.

### INV-018 Intensity summary per reporting period
- Predicate:
```omn
∃ g ∈ Granularity • ∀ c ∈ Ctx • c.granularity = g ⇒ reportedPerPeriod(c, {m : IntensitySummary | m.scale ≠ ∅}, allTypes)
```
- Reading: Headache intensity is summarised per reporting period, on a stated scale.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-010
- Evidence: Stage 1 OUT-010.

### INV-019 Duration summary per reporting period
- Predicate:
```omn
∃ g ∈ Granularity • ∀ c ∈ Ctx • c.granularity = g ⇒ reportedPerPeriod(c, {m : DurationSummary | m.kind ≠ auraDuration}, allTypes)
```
- Reading: Attack or headache duration is summarised per reporting period.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-011
- Evidence: Stage 1 OUT-011.

### INV-020 Durations of treated attacks are labelled as influenced by acute treatment
- Predicate:
```omn
∀ d : DurationSummary • d.kind ≠ auraDuration ∧ d.attackScope ≠ untreatedAttacks ⇒ annotated(d, durationInfluencedByAcuteTreatment)
```
- Reading: A duration summary that covers acutely treated attacks carries the label that durations of treated attacks are influenced by acute treatment.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-011
- Evidence: Stage 1 OUT-011.

### INV-021 Durations of treated attacks are not a stand-alone efficacy measure
- Predicate:
```omn
¬ ∃ d : DurationSummary • d.kind ≠ auraDuration ∧ d.attackScope ≠ untreatedAttacks ∧ standAloneEfficacyMeasure ∈ d.claims
```
- Reading: A duration summary that covers acutely treated attacks is not presented as a stand-alone measure of treatment efficacy.
- Conformance: SHOULD NOT. Scope: output.
- Realises: OUT-011
- Evidence: Stage 1 OUT-011 Caveats ("The output should therefore not present duration of treated attacks as a stand-alone efficacy measure").

### INV-022 Associated symptoms and most bothersome symptom across periods, for migraine
- Predicate:
```omn
∃ g ∈ Granularity • ∀ c ∈ Ctx • c.granularity = g ∧ hasType(c, c1) ⇒
  (∀ s : AssociatedSymptom • reportedPerPeriod(c, {m : AssociatedSymptomSummary | m.symptom = s}, allTypes)) ∧
  reportedPerPeriod(c, MostBothersomeSymptomItem, allTypes)
```
- Reading: For migraine, the presence of nausea/vomiting, photophobia and phonophobia and the most bothersome symptom are reported across periods.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-012
- Evidence: Stage 1 OUT-012.

### INV-023 Acute-medication days per reporting period: total, by class and by drug
- Predicate:
```omn
∃ g ∈ Granularity • ∀ c ∈ Ctx • c.granularity = g ⇒ reportedTogether(c,
  {TotalAcuteMedicationDays} ∪
  {m ∈ c.subject.acuteMedications • {d : DayCount | d.measure = acuteMedicationDays(ofClass(classOf(m.drug)))}} ∪
  {m ∈ c.subject.acuteMedications • {d : DayCount | d.measure = acuteMedicationDays(ofDrug(m.drug))}}, allTypes)
```
- Reading: For every period of the selected time range, one view shows the days with acute medication in total across classes, for each ICHD-3 8.2 class of the subject's acute medications, and for each individual drug.
- Conformance: MUST. Scope: repertoire.
- Realises: OUT-014
- Evidence: Stage 1 OUT-014.

### INV-024 Totals, classes and drugs agree
- Predicate:
```omn
∀ v : View; p : Period; sc : TypeScope •
  (∀ k : AcuteDrugClass; t ∈ daysOf(v, acuteMedicationDays(allAcuteMedication), p, sc); n ∈ daysOf(v, acuteMedicationDays(ofClass(k)), p, sc) • n ≤ t) ∧
  (∀ dr ∈ dom classOf; n ∈ daysOf(v, acuteMedicationDays(ofDrug(dr)), p, sc); k ∈ daysOf(v, acuteMedicationDays(ofClass(classOf(dr))), p, sc) • n ≤ k) ∧
  (∀ ks : set1 AcuteDrugClass; u ∈ daysOf(v, acuteMedicationDays(ofClasses(ks)), p, sc) •
     (∀ k ∈ ks; n ∈ daysOf(v, acuteMedicationDays(ofClass(k)), p, sc) • n ≤ u) ∧
     (∀ t ∈ daysOf(v, acuteMedicationDays(allAcuteMedication), p, sc) • u ≤ t) ∧
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
- Reading: In one view, for the same period and type scope: the days with any acute medication are at least the days with each class; the days with a class are at least the days with each drug of that class; the days with any medication of a set of classes (the 8.2.6 basis) lie between the largest value of its classes and the sum of their values, and do not exceed the total; when every class of the subject's acute medications is shown, the total does not exceed the sum of the class values; and when every drug of a class is shown, the class value does not exceed the sum of the drug values. A day with medication of two classes counts once in the total and once in each class, so the total is in general smaller than the sum.
- Conformance: definitional (E-029). Scope: output.
- Realises: OUT-014, OUT-016
- Evidence: Stage 1 OUT-014 ("broken down by drug class [...] and by individual drug, together with the total across classes"), OUT-016.

### INV-025 Weekly view of acute-medication days
- Predicate:
```omn
∀ c ∈ Ctx • c.granularity = calendarWeek ⇒ ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views •
  v ∈ WeeklyMedicationView ∧ ∃ sr ∈ v.content ∩ Series • tiles(sr, c.timeRange, calendarWeek) ∧ perPeriod(v, sr, TotalAcuteMedicationDays, allTypes)
```
- Reading: Acute-medication days are available per calendar week for every week of the selected time range, in addition to the per-period totals.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-015
- Evidence: Stage 1 OUT-015.

### INV-026 Functional impact per reporting period
- Predicate:
```omn
∃ g ∈ Granularity • ∀ c ∈ Ctx • c.granularity = g ⇒ reportedTogether(c,
  {fiDays(paidWorkOrSchool, affected), fiDays(householdWork, affected), fiDays(socialOrLeisure, affected),
   {m : DayCount | ∃ d : ImpactDomain • m.measure = functionalImpactDays((d, severelyImpaired))}}, allTypes)
```
- Reading: Per reporting period, the days on which headache affected paid work or school, household work, and social or leisure activities, and the days with severe functional impairment, are shown together, in days per period.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-027
- Evidence: Stage 1 OUT-027.

### INV-027 Functional impact compared with the baseline period
- Predicate:
```omn
∀ c ∈ Ctx; t ∈ c.subject.preventiveTreatments • startOf(c, t) ≠ ∅ ⇒
  ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views; rc ∈ v.content ∩ ResponseComparison • rc.treatment = t ∧
    ∀ p ∈ {rc.baseline} ∪ ran rc.onTreatment •
      (∀ d ∈ {paidWorkOrSchool, householdWork, socialOrLeisure} • ∃ m ∈ v.content ∩ fiDays(d, affected) • m.period = p ∧ m.typeScope = allTypes) ∧
      (∃ m ∈ v.content ∩ DayCount • m.period = p ∧ m.typeScope = allTypes ∧ ∃ d : ImpactDomain • m.measure = functionalImpactDays((d, severelyImpaired)))
```
- Reading: For each preventive treatment, functional impact can be shown for the pre-treatment baseline period and the on-treatment periods, next to the response comparison: for each of these periods, the days on which headache affected paid work or school, household work and social or leisure activities, and the days with severe functional impairment.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-027
- Evidence: Stage 1 OUT-027 ("including days with severe functional impairment, expressed in days per period, and SHOULD allow comparison with the baseline period").

### INV-028 Separate presentation per headache type
- Predicate:
```omn
∃ g ∈ MonthlyKind • ∀ c ∈ Ctx • c.granularity = g ∧ #c.subject.possibleHeadacheTypes ≥ 2 ⇒
  ∀ sc ∈ {allTypes} ∪ {t ∈ c.subject.possibleHeadacheTypes • ofType(t)} •
    reportedTogether(c, {HeadacheDays, TotalAcuteMedicationDays} ∪
      {m ∈ c.subject.acuteMedications • {d : DayCount | d.measure = acuteMedicationDays(ofClass(classOf(m.drug)))}} ∪
      {m ∈ c.subject.acuteMedications • {d : DayCount | d.measure = acuteMedicationDays(ofDrug(m.drug))}} ∪
      {K ∈ {ModerateSevereHeadacheDays, AttackCount} | provides(K)}, sc)
```
- Reading: When the subject has, or may have, more than one headache type, headache days, acute-medication days (in total, for each ICHD-3 8.2 class of the subject's acute medications and for each of their drugs), and moderate/severe headache days and attacks where the diary provides them, are shown for every period separately for each headache type and combined.
- Conformance: MUST. Scope: repertoire.
- Realises: OUT-029
- Evidence: Stage 1 OUT-029 ("frequency and acute medication outputs separately for each headache type"); the acute-medication outputs of OUT-014 ("broken down by drug class [...] and by individual drug, together with the total across classes"), as in INV-023.
- Notes: Migraine days are by definition migraine-specific and are not broken down further by type. "Acute medication outputs" is read as the acute-medication days of OUT-014 (total, per class and per drug); the weekly view (OUT-015, INV-025) and the medication-overuse indicator (OUT-016, INV-044) are required for all headache types combined; see ISS-09.

### INV-029 Intensity per headache type, where provided
- Predicate:
```omn
∃ g ∈ Granularity • ∀ c ∈ Ctx • c.granularity = g ∧ #c.subject.possibleHeadacheTypes ≥ 2 ∧ provides(IntensitySummary) ⇒
  ∀ t ∈ c.subject.possibleHeadacheTypes • reportedPerPeriod(c, IntensitySummary, ofType(t))
```
- Reading: Where the intensity summary is provided and the subject has, or may have, more than one headache type, it is also shown separately for each type.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-029
- Evidence: Stage 1 OUT-029.

### INV-030 Values per headache type do not exceed the combined values
- Predicate:
```omn
(∀ v : View; p : Period; h : HeadacheType; k : DayMeasure •
   (k ∈ {headacheDays, migraineDays, moderateSevereHeadacheDays} ∨ k is acuteMedicationDays) ⇒
     ∀ a ∈ daysOf(v, k, p, ofType(h)); b ∈ daysOf(v, k, p, allTypes) • a ≤ b) ∧
(∀ v : View • ∀ e, f ∈ v.content ∩ EventCount • e.event = f.event ∧ e.period = f.period ∧ (∃ h : HeadacheType • e.typeScope = ofType(h)) ∧
   f.typeScope = allTypes ⇒ e.count ≤ f.count)
```
- Reading: In one view and period, the headache days, migraine days, moderate/severe headache days and acute-medication days of one headache type, and its attacks and auras, do not exceed the values for all types combined.
- Conformance: definitional (E-012, E-014, E-019). Scope: output.
- Realises: OUT-029
- Evidence: Stage 1 OUT-029.

### INV-031 Relations between day measures
- Predicate:
```omn
∀ v : View; p : Period; sc : TypeScope •
  (∀ a ∈ daysOf(v, moderateSevereHeadacheDays, p, sc); b ∈ daysOf(v, headacheDays, p, sc) • a ≤ b) ∧
  (∀ a ∈ daysOf(v, headacheFreeDays, p, sc); b ∈ daysOf(v, headacheDays, p, sc) • a + b ≤ p.lengthDays) ∧
  (∀ a ∈ daysOf(v, symptomFreeDays, p, sc); b ∈ daysOf(v, headacheFreeDays, p, sc) • a ≤ b) ∧
  (∀ u ∈ daysOf(v, migraineOrModerateSevereHeadacheDays, p, sc); a ∈ daysOf(v, migraineDays, p, sc);
       b ∈ daysOf(v, moderateSevereHeadacheDays, p, sc) • a ≤ u ∧ b ≤ u ∧ u ≤ a + b) ∧
  (∀ n ∈ daysOf(v, migraineDays, p, sc) •
     (∃ mk ∈ v.content ∩ MigraineFreePeriodMark • mk.period = p ∧ mk.typeScope = sc) ⇒ n = 0) ∧
  ((∃ mk ∈ v.content ∩ MigraineFreePeriodMark • mk.typeScope = sc) ∧ 0 ∈ daysOf(v, migraineDays, p, sc) ⇒
     ∃ mk ∈ v.content ∩ MigraineFreePeriodMark • mk.period = p ∧ mk.typeScope = sc)
```
- Reading: In one view, for the same period and scope: moderate/severe headache days do not exceed headache days; headache-free days and headache days together do not exceed the period length; symptom-free days do not exceed headache-free days; days with migraine or moderate-to-severe headache lie between the larger of the migraine-day and moderate/severe-day counts and their sum; a period marked as without migraine days shows no migraine days, and a view that marks such periods marks every period whose migraine-day count is 0.
- Conformance: definitional (E-017, E-018, E-020, E-021, E-022). Scope: output.
- Realises: OUT-006, OUT-008, OUT-020
- Evidence: Stage 1 OUT-008 (symptom-free days defined as "the days free of premonitory, aura, headache, and postdromal symptoms" [S-002]), OUT-006, OUT-020; [S-010] the count of E-018.
- Notes: The relations are inequalities: days without diary information are neither headache days nor headache-free days, and the definitions say nothing about them. Migraine days are not related to headache days because published migraine-day definitions differ (OUT-002).

### INV-032 Intensity values lie on their scale
- Predicate:
```omn
∀ i : IntensitySummary •
  (∀ s ∈ i.scale • (∀ j ∈ dom s.points • j < #s.points ⇒ s.points(j).score < s.points(j + 1).score) ∧
     (∀ ds : set1 LevelDays • i.summary = peakIntensityDistribution(ds) ⇒ ∀ ld ∈ ds • ld.level ∈ ran s.points) ∧
     (∀ q : ℚ • i.summary = meanPeakIntensity(q) ⇒ first(s.points).score ≤ q ∧ q ≤ last(s.points).score)) ∧
  (∀ ds : set1 LevelDays • i.summary = peakIntensityDistribution(ds) ⇒
     (∀ ld ∈ ds • ld.days ≤ i.period.lengthDays) ∧
     (∀ ld₁, ld₂ ∈ ds • ld₁.level = ld₂.level ⇒ ld₁ = ld₂) ∧
     (∀ h ∈ daysOf(viewOf(i), headacheDays, i.period, i.typeScope) • (Σ ld ∈ ds • ld.days) ≤ h))
```
- Reading: The points of a scale are in increasing order; a distribution uses levels of the stated scale, once each, and its counts, individually and together, do not exceed the period length or the headache days shown for the same period and scope; a mean peak intensity lies within the scale.
- Conformance: definitional (E-023). Scope: output.
- Realises: OUT-010
- Evidence: Stage 1 OUT-010 ("the distribution of headache days by peak intensity category, or an average peak intensity on the scale used").

### INV-033 Further bounds of per-period values
- Predicate:
```omn
(∀ d : DurationSummary • d.kind = moderateSeverePainTime ∧ d.statistic = total ⇒ d.value ≤ daysLong(d.period.lengthDays)) ∧
(∀ a : AssociatedSymptomSummary •
   (∀ n : ℕ • a.presence = daysWithSymptom(n) ⇒ n ≤ a.period.lengthDays) ∧
   (∀ n : ℕ; e ∈ viewOf(a).content ∩ AttackCount • a.presence = attacksWithSymptom(n) ∧ e.period = a.period ∧ e.typeScope = a.typeScope ⇒ n ≤ e.count)) ∧
(∀ v : View; p : Period; sc : TypeScope; d : ImpactDomain; s ∈ {missed, impaired, severelyImpaired} •
   ∀ a ∈ daysOf(v, functionalImpactDays((d, s)), p, sc); b ∈ daysOf(v, functionalImpactDays((d, affected)), p, sc) • a ≤ b) ∧
(∀ ci : CaregiverImpact • ∀ n : ℕ • ci.impact = caregiverLostProductiveDays(n) ⇒ n ≤ ci.period.lengthDays)
```
- Reading: The total time with moderate/severe pain does not exceed the length of the period; days with an associated symptom do not exceed the period length and attacks with it do not exceed the attacks shown; days missed, impaired or severely impaired in a domain do not exceed the days affected in that domain; a caregiver's lost productive days do not exceed the period length.
- Conformance: definitional (E-024, E-025, E-030, E-031). Scope: output.
- Realises: OUT-011, OUT-012, OUT-027, OUT-036
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
∀ v : TimeCourseView • v.series ∈ v.content ∧ v.covers.start = first(v.series.periods).start ∧ v.covers.end = last(v.series.periods).end ∧
  perPeriod(v, v.series, HeadacheDays, allTypes) ∧ (hasType(ctx, c1) ⇒ perPeriod(v, v.series, MigraineDays, allTypes)) ∧
  perPeriod(v, v.series, ModerateSevereHeadacheDays, allTypes) ∧ perPeriod(v, v.series, AttackCount, allTypes) ∧
  ∀ e ∈ ctx.subject.courseEvents • e.treatment ∈ ctx.subject.preventiveTreatments ∧ markedKind(e.kind) ∧
    v.covers.start ≤ e.date ∧ e.date ≤ v.covers.end ⇒
      ∃ mk ∈ v.markers • mk.treatment = e.treatment ∧ mk.event = e.kind ∧ mk.date = e.date
```
- Reading: A time-course view shows headache days, migraine days (for patients with migraine), moderate/severe headache days and attacks for every period of its series, and a dated marker for every start, dose change and stop of a preventive treatment within the period it covers.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-009
- Evidence: Stage 1 OUT-009 ("frequency measures (OUT-004 to OUT-007) as a time series of consecutive reporting periods [...] with dated markers for the start, dose change and stop of preventive treatments"). Migraine days keep the OUT-005 condition (section 3.5, reference rule).

### INV-036 Markers show the treatment course
- Predicate:
```omn
∀ mk : TreatmentMarker • markedKind(mk.event) ∧ mk.treatment ∈ ctx.subject.preventiveTreatments ∧ eventOn(ctx, mk.treatment, mk.event, mk.date)
```
- Reading: A marker shows a start, dose change or stop of one of the subject's preventive treatments on the date it occurred.
- Conformance: definitional (E-034). Scope: output.
- Realises: OUT-009
- Evidence: Stage 1 OUT-009.

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
- Reading: For any selection of two or more periods of equal length (for example a baseline period and a later period of the same length), the diary can show the frequency measures for exactly those periods side by side.
- Conformance: MUST. Scope: repertoire.
- Realises: OUT-001
- Evidence: Stage 1 OUT-001 ("the output MUST allow comparison of periods of equal length").

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
  (c.subject.ageGroup = childOrAdolescent ⇒ ∀ r, s ∈ ran c.comparedSpans • days(r.from, r.to) = days(s.from, s.to)) ⇒
  ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views; pc ∈ v.content ∩ PeriodComparison •
    matchesSelection(pc, c) ∧ ∀ p ∈ ran pc.periods • ∃ m ∈ pc.values ∩ IntensitySummary • m.period = p ∧ m.scale ≠ ∅
```
- Reading: Intensity summaries, with their scale, can be compared between selected periods; for children and adolescents, between selected periods of equal length.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-010
- Evidence: Stage 1 OUT-010 ("and allow comparison between periods"); OUT-036 (c) ("apply equal-length period comparisons as in OUT-001") for children and adolescents.
- Notes: For children and adolescents, every comparison SHOULD compare periods of equal length (INV-097, OUT-036 (c)). OUT-010 asks only that comparison between periods be allowed and names no lengths, so for these subjects a comparison of selected periods of equal length allows it; requiring a comparison of a selection of unequal lengths as well would contradict INV-097.

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
∀ v : ThreeMonthPatternView • v.series ∈ v.content ∧ #v.series.periods = 3 ∧ v.series.granularity ∈ MonthlyKind ∧
  mostRecent(v.series, ctx.asOf) ∧ v.covers.start = first(v.series.periods).start ∧ v.covers.end = last(v.series.periods).end
```
- Reading: The view shows three consecutive monthly periods, the most recent ones that end on or before the as-of date, and covers exactly those.
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

### INV-043 Three-month view assigns no diagnosis
- Predicate:
```omn
¬ ∃ v : ThreeMonthPatternView; x ∈ {v} ∪ v.content; d : DiagnosisRef • diagnosis(d) ∈ x.claims
```
- Reading: Neither the three-month view nor anything shown in it presents the subject as having a diagnosis.
- Conformance: SHOULD NOT. Scope: output.
- Realises: OUT-028, OUT-038
- Evidence: Stage 1 OUT-028 ("it SHOULD NOT itself assign a diagnosis (see OUT-038)").

### 6.5 Medication overuse and withdrawal

### INV-044 Medication-overuse indicator per period, per class and for combined use
- Predicate:
```omn
∃ g ∈ MonthlyKind • ∀ c ∈ Ctx • c.granularity = g ⇒ ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views; sr ∈ v.content ∩ Series •
  tiles(sr, c.timeRange, g) ∧ ∀ p ∈ ran sr.periods •
    ∀ s ∈ {m ∈ c.subject.acuteMedications • ofClassUse(classOf(m.drug))} ∪ {combinedUse} •
      ∃ i ∈ v.content ∩ MedicationOveruseIndicator • i.period = p ∧ i.scope = s
```
- Reading: For every calendar month or 28-day period of the selected time range, the output indicates, for each class of the subject's acute medications and for the combined use of ICHD-3 8.2.6, whether acute medication use reached the ICHD-3 level of regular use over the time span the code refers to.
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
- Notes: The span is the shortest one so that the indication of a period is unambiguous; with calendar months or 28-day periods it has four periods.

### INV-046 Combined use of ICHD-3 8.2.6
- Predicate:
```omn
∀ i : MedicationOveruseIndicator • i.scope = combinedUse ⇒
  (i.status = levelReached ⇒ (∀ j ∈ dom i.basis • i.basis(j).days ≥ i.referenceLevel) ∧
     ¬ ∃ i₂ : MedicationOveruseIndicator • i₂.period = i.period ∧ i₂.status = levelReached ∧
         ∃ k ∈ classesOf821to825 • i₂.scope = ofClassUse(k)) ∧
  ((∀ j ∈ dom i.basis • i.basis(j).days ≥ i.referenceLevel) ∧
   (∀ k ∈ classesOf821to825 • (∃ m ∈ ctx.subject.acuteMedications • classOf(m.drug) = k) ⇒
      ∃ i₂ : MedicationOveruseIndicator • i₂.period = i.period ∧ i₂.scope = ofClassUse(k) ∧ i₂.status = levelNotReached)
   ⇒ i.status = levelReached)
```
- Reading: The combined-use indication is "reached" only if the days with any medication of the 8.2.6 classes reach 10 in every period of the span and no class of 8.2.1–8.2.5 reaches its own level for the same period; when the combined days reach the level in every period and every class of 8.2.1–8.2.5 that the subject uses is shown as not reached, the combined indication is "reached".
- Conformance: definitional (E-032). Scope: output.
- Realises: OUT-016
- Evidence: Stage 1 OUT-016 ("for ICHD-3 subtype 8.2.6, for the combined use of acute medication across classes"); [S-001] 8.2.6 criterion B and note 2 quoted in E-028.

### INV-047 Indicator worded as a prompt for clinical review
- Predicate:
```omn
∀ i : MedicationOveruseIndicator • annotated(i, reviewPromptPossibleMedicationOveruse)
```
- Reading: Every medication-overuse indicator is worded as a prompt for clinical review of possible medication overuse.
- Conformance: MUST. Scope: output.
- Realises: OUT-016
- Evidence: Stage 1 OUT-016.

### INV-048 Indicator is not a diagnosis of medication-overuse headache
- Predicate:
```omn
¬ ∃ i : MedicationOveruseIndicator; t : ICHD3Code • t ⊑ c8_2 ∧
  (diagnosis(headacheDiagnosis(t)) ∈ i.claims ∨ ∃ a : Annotation • i ∈ a.qualifies ∧ diagnosis(headacheDiagnosis(t)) ∈ a.claims)
```
- Reading: Neither the indicator nor any label qualifying it presents the subject as having medication-overuse headache or one of its subtypes.
- Conformance: MUST NOT. Scope: output.
- Realises: OUT-016
- Evidence: Stage 1 OUT-016 ("MUST NOT be presented as a diagnosis of medication-overuse headache").

### INV-049 Withdrawal follow-up view available
- Predicate:
```omn
∀ c ∈ Ctx; ws ∈ c.subject.withdrawalStart • c.timeRange.from = ws ∧ c.timeRange.to ≤ plusMonths(ws, followUpMonths) ⇒
  ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ WithdrawalFollowUpView • v.withdrawalStart = ws ∧
    tiles(v.series, c.timeRange, c.granularity)
```
- Reading: For a subject withdrawing from overused medication, the follow-up view is available for every time range that starts at the start of withdrawal and ends within the following year.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-017
- Evidence: Stage 1 OUT-017.

### INV-050 Withdrawal follow-up content
- Predicate:
```omn
∀ v : WithdrawalFollowUpView • v.series ∈ v.content ∧ v.withdrawalStart ∈ ctx.subject.withdrawalStart ∧
  first(v.series.periods).start = v.withdrawalStart ∧
  perPeriod(v, v.series, HeadacheDays, allTypes) ∧ perPeriod(v, v.series, TotalAcuteMedicationDays, allTypes) ∧
  (plusDays(v.withdrawalStart, 7 × reviewWindowToWeeks) ≤ last(v.series.periods).end ⇒ v.reviewWindow ≠ ∅)
```
- Reading: The view shows headache days and acute-medication days for every period from the start of withdrawal onward and, once its periods reach the end of the NICE review window, the review window.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-017
- Evidence: Stage 1 OUT-017.

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

### INV-052 Label of the expected transient worsening
- Predicate:
```omn
∀ v : WithdrawalFollowUpView • annotated(v, expectedTransientWorseningEarlyWithdrawal)
```
- Reading: The withdrawal follow-up view labels the transient worsening expected in the early withdrawal phase.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-017
- Evidence: Stage 1 OUT-017.

### 6.6 Preventive treatment response

### INV-053 Absolute and percentage change agree with the values they compare
- Predicate:
```omn
∀ ch : Change • ch.reference.measure = ch.compared.measure ∧ ch.reference.typeScope = ch.compared.typeScope ∧
  ch.reference.period ≠ ch.compared.period ∧ ch.absolute = ch.compared.days − ch.reference.days ∧
  (ch.reference.days > 0 ⇒ ∃ q : ℚ • ch.relative = percent(q) ∧ q ≈ 100 × ch.absolute ÷ ch.reference.days) ∧
  (ch.reference.days = 0 ⇒ ch.relative = undefinedForZeroReference)
```
- Reading: A change compares two values of the same measure and scope for two different periods; the absolute change is the compared value minus the reference value, and the percentage change is the absolute change divided by the reference value, in per cent, or is shown as not defined when the reference value is 0.
- Conformance: definitional (E-040). Scope: output.
- Realises: OUT-018
- Evidence: Stage 1 OUT-018 ("the absolute and percentage change from baseline").

### INV-054 A change is shown with the values it compares
- Predicate:
```omn
∀ ch : Change • ch.reference ∈ viewOf(ch).content ∧ ch.compared ∈ viewOf(ch).content
```
- Reading: An absolute or percentage change is shown together with the two values it compares.
- Conformance: MUST. Scope: output.
- Realises: OUT-018, OUT-020
- Evidence: Stage 1 OUT-018 ("showing both the values of each period and the absolute and percentage change from baseline").

### INV-055 Response comparison for each preventive treatment, at the evaluation time points
- Predicate:
```omn
∀ c ∈ Ctx; t ∈ c.subject.preventiveTreatments •
  (startOf(c, t) ≠ ∅ ⇒ ∃ o : Output • (c, o) ∈ Rep ∧ ∃ x ∈ parts(o) ∩ ResponseComparison • x.treatment = t) ∧
  (∀ r ∈ evaluationRules; a ∈ anchorDates(c, t, r.anchor); s ∈ startOf(c, t) •
     applicable(c, t, r) ∧ shift(a, r.minOffset) ≤ c.asOf ∧ fitsMonthlyPeriod(s, a, r) ⇒
       ∃ o : Output • (c, o) ∈ Rep ∧ ∃ x ∈ parts(o) ∩ ResponseComparison • x.treatment = t ∧
         equalLengths({x.baseline} ∪ ran x.onTreatment) ∧
         ∃ tp ∈ x.timePoints; p ∈ ran x.onTreatment • tp.rule = r ∧ tp.anchorDate = a ∧ atTimePoint(p, tp))
```
- Reading: For each preventive treatment that has started, a response comparison is available. For each evaluation time point that current guidance names for the treatment's type, that has been reached by the as-of date, and at which a calendar month or 28-day period beginning on or after the treatment start can end (for a window, within the window), a comparison of periods of equal length is available whose on-treatment period ends at that time point (within that window).
- Conformance: MUST. Scope: repertoire.
- Realises: OUT-001, OUT-018, OUT-036
- Evidence: Stage 1 OUT-018 ("The output MUST allow this comparison at the evaluation time points named in current guidance"), OUT-001 ("for example a pre-treatment baseline period against a later period of the same length"), OUT-036 (d) (efficacy of treatment from diary data, for children and adolescents; the MUST of OUT-018 covers every subject).
- Notes: The on-treatment periods of a comparison are calendar months or 28-day periods that begin on or after the treatment start (INV-056), so none ends less than 27 days after the start. A time point earlier than that cannot be the end of such a period, and the comparison is not required at it (`fitsMonthlyPeriod`, E-042). Because no course event precedes the start (INV-001), this can happen only for NICE CG150 1.3.29, whose time point is the end of the second treatment cycle (E-041 Notes). Satisfiability: for a time point that fits, a 28-day on-treatment period that ends at the time point (for a window, at the later of its earliest date and the 27th day after the start, which the condition places within the window) begins on or after the start, and a 28-day baseline period that ends before the start has the same length; so INV-055, INV-056 and, for children and adolescents, INV-097 hold together in every admissible context.

### INV-056 Response comparison content
- Predicate:
```omn
∀ rc : ResponseComparison • rc.treatment ∈ ctx.subject.preventiveTreatments ∧ rc.treatmentStart ∈ startOf(ctx, rc.treatment) ∧
  rc.baseline.kind ∈ MonthlyKind ∧ (∀ p ∈ ran rc.onTreatment • p.kind ∈ MonthlyKind) ∧
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
- Reading: A response comparison is aligned to the treatment's start date: its baseline is a calendar month or 28-day period that ends before the start, and its on-treatment periods are calendar months or 28-day periods that begin on or after the start, in order. For the baseline and every on-treatment period it shows headache days and migraine days, which are therefore monthly values, and for every on-treatment period the change of each from baseline. Every change it shows compares a value it shows for an on-treatment period with the value it shows for the baseline.
- Conformance: MUST. Scope: output.
- Realises: OUT-018
- Evidence: Stage 1 OUT-018 ("compare monthly migraine days and monthly headache days [...] in a pre-treatment baseline period with periods after treatment start"); OUT-001 (the monthly periods: calendar months or 28-day periods).

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
  tp.anchorDate ∈ anchorDates(ctx, tp.treatment, tp.rule.anchor) ∧ tp.earliest = shift(tp.anchorDate, tp.rule.minOffset) ∧
  (∀ x ∈ tp.rule.maxOffset • tp.latest = {shift(tp.anchorDate, x)}) ∧ (tp.rule.maxOffset = ∅ ⇒ tp.latest = ∅)
```
- Reading: A time point belongs to a guidance rule that applies to the treatment's type; its anchor date is the treatment's start, the date the tolerated or target dose was reached, or the end of the stated treatment cycle; its date (or window) is the anchor date shifted by the rule's offset(s).
- Conformance: definitional (E-042). Scope: output.
- Realises: OUT-018
- Evidence: Stage 1 OUT-018 (see E-041).

### INV-059 Evaluation time points shown with the comparison
- Predicate:
```omn
∀ rc : ResponseComparison • (∀ tp ∈ rc.timePoints • tp.treatment = rc.treatment ∧ tp ∈ viewOf(rc).content) ∧
  ∀ r ∈ evaluationRules; a ∈ anchorDates(ctx, rc.treatment, r.anchor) • applicable(ctx, rc.treatment, r) ⇒
    ∃ tp ∈ rc.timePoints • tp.rule = r ∧ tp.anchorDate = a
```
- Reading: Every response comparison shows, in its view, the evaluation time points of all guidance rules that apply to the treatment.
- Conformance: MUST. Scope: output.
- Realises: OUT-018
- Evidence: Stage 1 OUT-018.

### INV-060 Residual burden next to a percentage change
- Predicate:
```omn
∀ ch : Change • ch.reference.measure ∈ {migraineDays, headacheDays} ∧ ch.relative is percent ⇒
  ∃ rb ∈ viewOf(ch).content ∩ ResidualBurden • rb.change = ch ∧ rb.migraineDays ∈ viewOf(ch).content ∧
    rb.moderateSevereHeadacheDays ∈ viewOf(ch).content
```
- Reading: Wherever a percentage change in migraine or headache days is shown, the absolute numbers of migraine days and moderate/severe headache days per month that remain on treatment are shown next to it.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-019
- Evidence: Stage 1 OUT-019.

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
  (∃ rc ∈ L.comparison • rc.treatment = L.treatment ∧ rc ∈ viewOf(L).content ∧ ran L.evaluated ⊆ ran rc.onTreatment ∧
     ∀ ch ∈ rc.changes • ch.compared.period ∈ ran L.evaluated ∧ ch.relative is percent ∧ ch.reference.measure ∈ {migraineDays, headacheDays} ⇒
       ∃ rb ∈ L.residual • rb.change = ch) ∧
  (∀ x ∈ L.otherValues • x ∈ viewOf(L).content) ∧ (∀ rb ∈ L.residual • rb ∈ viewOf(L).content) ∧
  (∀ K ∈ L.criterion; u ∈ K.alsoRestsOn • valueAvailable(ctx, u) ⇒
     (∀ ins : Instrument • u = instrumentResultOf(ins) ⇒ ∃ r ∈ L.otherValues ∩ InstrumentResult • r.instrument = ins) ∧
     (u = acuteTreatmentEffectiveness ⇒ ∃ s ∈ L.otherValues ∩ AcuteTreatmentSummary • s.period ∈ ran L.evaluated)) ∧
  (∀ x : ControlLevel • L.category = controlLevel(x) ⇒ ∀ p ∈ ran L.evaluated • levelDays(L, p) ≠ ∅)
```
- Reading: A responder label names the criterion it applies, with its thresholds; it is shown with the response comparison of its treatment and the residual burden of the changes it refers to, and with the instrument results, global-impression results and acute-treatment effectiveness on which the named criterion also rests, where results of the instrument are available or the subject uses acute medication; a control-level label is shown with the days with migraine or moderate-to-severe headache of each evaluated month.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-019, OUT-020
- Evidence: Stage 1 OUT-020; [S-010] for the count on which the control levels rest (E-018). The other values keep the applicability conditions of the requirements OUT-020 refers to (section 3.5, reference rule): OUT-026 ("Where results of validated instruments are available") and OUT-023 ("For each acute medication").
- Notes: An instrument result SHOULD show its completion date (E-058), and that date is the date of an available result (INV-082); a result of an instrument for which no result is available therefore cannot be shown. Without the availability condition, a label under a criterion that rests on such an instrument (for example IHS Q6, which also rests on PGIC, MIDAS and HIT-6) could not satisfy this invariant together with E-058 and INV-082.

### INV-063 A responder label agrees with the decidable components of its criterion
- Predicate:
```omn
∀ L : ResponderLabel; K ∈ L.criterion •
  (controlLevels ∈ K.components ⇔ L.category is controlLevel) ∧
  ((L.category = responder ∨ L.category = nonResponder) ⇒
     ((∃ k ∈ K.components • componentMet(L, k)) ⇒ L.category = responder) ∧
     ((∀ k ∈ K.components • componentDecided(L, k) ∧ ¬ componentMet(L, k)) ⇒ L.category = nonResponder))
```
- Reading: If any component of the named criterion is met by the values shown (a reduction from baseline of at least the threshold in one of its measures, in the single on-treatment period the label refers to, or an instrument-score decrease of at least the threshold from a baseline in the stated range, for subjects meeting the component's condition), the label is "responder". If every component can be decided from the values shown and none is met, the label is "non-responder". A criterion with a judgement component is not decided by the values alone, so the model then requires only the first relation. A reduction component is decided only for a label that refers to one on-treatment period, because the cited criteria do not state how several periods are combined; a label over several periods is not decided by its reduction components.
- Conformance: definitional (E-046). Scope: output.
- Realises: OUT-020
- Evidence: Stage 1 OUT-020; thresholds quoted in E-045.

### INV-064 Control levels of the IHS position statement 2025
- Predicate:
```omn
∀ L : ResponderLabel; x : ControlLevel • L.category = controlLevel(x) ⇒
  (∀ p ∈ ran L.evaluated • p.kind ∈ MonthlyKind) ∧ consecutive(L.evaluated) ∧
  (x = migraineFreedom ⇒ ∀ p ∈ ran L.evaluated; n ∈ levelDays(L, p) • n = 0) ∧
  (x = optimalControl ⇒ #L.evaluated ≥ 3 ∧ ∀ p ∈ ran L.evaluated; n ∈ levelDays(L, p) • n < 4) ∧
  (x = modestControl ⇒ ∀ p ∈ ran L.evaluated; n ∈ levelDays(L, p) • 4 ≤ n ∧ n ≤ 6) ∧
  ((∀ p ∈ ran L.evaluated • ∃ n ∈ levelDays(L, p) • n > 6) ⇒ x = insufficientControl)
```
- Reading: A control-level label refers to consecutive monthly periods. "Migraine freedom" shows no day with migraine or moderate-to-severe headache in any evaluated month; "optimal control" shows fewer than four such days in each of at least three evaluated months; "modest control" shows four to six in each; and when every evaluated month shows more than six, the level is "insufficient control". Insufficient control may also be shown with fewer days, as [S-010] allows.
- Conformance: definitional (E-046). Scope: output.
- Realises: OUT-020
- Evidence: Stage 1 OUT-020; [S-010] quoted in E-046.

### INV-065 A responder label is not the sole indicator of individual benefit
- Predicate:
```omn
¬ ∃ L : ResponderLabel • soleIndicatorOfIndividualBenefit ∈ L.claims
```
- Reading: No responder label is presented as the sole indicator of individual benefit.
- Conformance: SHOULD NOT. Scope: output.
- Realises: OUT-020
- Evidence: Stage 1 OUT-020 ("Responder labels SHOULD NOT be presented as the sole indicator of individual benefit").

### INV-066 Adherence next to the response comparison
- Predicate:
```omn
∀ rc : ResponseComparison • ∃ a ∈ viewOf(rc).content ∩ AdherenceSummary • a.treatment = rc.treatment ∧
  rc.treatmentStart ≤ a.window.start ∧ ∃ p ∈ ran rc.onTreatment • a.window.end = p.end
```
- Reading: Each response comparison is shown with the patient-reported adherence to the treatment over an evaluation window that begins on or after the treatment start and ends with one of its on-treatment periods.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-039
- Evidence: Stage 1 OUT-039.

### INV-067 Adherence refers to the time on treatment
- Predicate:
```omn
∀ a : AdherenceSummary • a.treatment ∈ ctx.subject.preventiveTreatments ∧ ∀ s ∈ startOf(ctx, a.treatment) • s ≤ a.window.start
```
- Reading: Adherence is shown for a preventive treatment and for a window that begins on or after its start.
- Conformance: definitional (E-047). Scope: output.
- Realises: OUT-039
- Evidence: Stage 1 OUT-039.

### INV-068 Treatment review view: frequency and medication for the same periods
- Predicate:
```omn
∀ v : TreatmentReviewView • v.treatment ∈ ctx.subject.preventiveTreatments ∧
  (∀ s ∈ startOf(ctx, v.treatment) • v.baseline.end < s ∧ ∀ p ∈ ran v.onTreatment • s ≤ p.start) ∧
  ∀ p ∈ {v.baseline} ∪ ran v.onTreatment • shownDay(v, headacheDays, p, allTypes) ∧
    (hasType(ctx, c1) ⇒ shownDay(v, migraineDays, p, allTypes)) ∧ shownDay(v, acuteMedicationDays(allAcuteMedication), p, allTypes) ∧
    ∀ m ∈ ctx.subject.acuteMedications • shownDay(v, acuteMedicationDays(ofClass(classOf(m.drug))), p, allTypes) ∧
      shownDay(v, acuteMedicationDays(ofDrug(m.drug)), p, allTypes)
```
- Reading: The treatment review view shows, for the same baseline and on-treatment periods, headache days, migraine days (for patients with migraine) and acute-medication days: in total across classes, for each ICHD-3 8.2 class of the subject's acute medications, and for each of their drugs.
- Conformance: MUST. Scope: output.
- Realises: OUT-021
- Evidence: Stage 1 OUT-021 (MUST for OUT-004, OUT-005 and OUT-014 together; OUT-005 keeps its condition by the reference rule of section 3.5); the acute-medication days of OUT-014 ("broken down by drug class [...] and by individual drug, together with the total across classes"), as in INV-023, INV-028 and INV-104.

### INV-069 Treatment review view: further dimensions where provided
- Predicate:
```omn
∀ v : TreatmentReviewView •
  (∀ p ∈ {v.baseline} ∪ ran v.onTreatment •
     (provides(ModerateSevereHeadacheDays) ⇒ shownDay(v, moderateSevereHeadacheDays, p, allTypes)) ∧
     (provides(AttackCount) ⇒ ∃ m ∈ v.content ∩ AttackCount • m.period = p ∧ m.typeScope = allTypes) ∧
     (provides(IntensitySummary) ⇒ ∃ m ∈ v.content ∩ IntensitySummary • m.period = p) ∧
     (hasType(ctx, c1) ∧ provides(AssociatedSymptomSummary) ⇒ ∀ s : AssociatedSymptom •
        ∃ m ∈ v.content ∩ AssociatedSymptomSummary • m.period = p ∧ m.symptom = s) ∧
     (hasType(ctx, c1) ∧ provides(MostBothersomeSymptomItem) ⇒ ∃ m ∈ v.content ∩ MostBothersomeSymptomItem • m.period = p) ∧
     (provides(AcuteTreatmentSummary) ⇒ ∀ am ∈ ctx.subject.acuteMedications •
        ∃ s ∈ v.content ∩ AcuteTreatmentSummary • s.drug = am.drug ∧ s.period = p)) ∧
  (provides(InstrumentResult) ⇒ ∀ i : Instrument •
     let A == {a ∈ ctx.subject.instrumentAdministrations | a.instrument = i ∧ a.date ≤ last(v.onTreatment).end • a.date} •
       A ≠ ∅ ⇒ ∃ r ∈ v.content ∩ InstrumentResult • r.instrument = i ∧ r.completionDate = {max A})
```
- Reading: Where the diary provides them, the treatment review view also shows, for the same periods, moderate/severe headache days, attacks, intensity, migraine-associated symptoms and the most bothersome symptom (for migraine), and the effectiveness of each acute medication for the attacks treated in each period, together with the most recent result of each instrument (including PGIC) up to the end of the last on-treatment period.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-021, OUT-023
- Evidence: Stage 1 OUT-021, OUT-023 ("so that a change in the response to acute treatment after the start of prevention is visible (see OUT-021)").

### INV-070 Post-stop monitoring content
- Predicate:
```omn
∀ v : PostStopMonitoringView • v.treatment ∈ ctx.subject.preventiveTreatments ∧
  (v.event is stop ∨ v.event = doseChange(reduction)) ∧ eventOn(ctx, v.treatment, v.event, v.eventDate) ∧
  (∀ b ∈ v.baseline; s ∈ startOf(ctx, v.treatment) • b.end < s) ∧
  (∀ q ∈ v.onTreatmentPeriod; s ∈ startOf(ctx, v.treatment) • s ≤ q.start ∧ q.end < v.eventDate) ∧
  consecutive(v.after) ∧ (v.after ≠ ∅ ⇒ first(v.after).start = v.eventDate) ∧
  ∀ p ∈ v.baseline ∪ v.onTreatmentPeriod ∪ ran v.after • shownDay(v, headacheDays, p, allTypes) ∧ shownDay(v, migraineDays, p, allTypes)
```
- Reading: After a stop, pause or dose reduction of a preventive treatment, the view shows headache days and migraine days for periods from that date onward, next to the same values for an on-treatment period before it and for the original pre-treatment baseline period, so that worsening or rebound above baseline is visible.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-022
- Evidence: Stage 1 OUT-022.

### 6.7 Acute treatment

### INV-071 Acute-treatment summaries per drug, per formulation and per preventive phase
- Predicate:
```omn
∀ c ∈ Ctx; m ∈ c.subject.acuteMedications •
  (∃ o : Output • (c, o) ∈ Rep ∧
     (∃ s ∈ parts(o) ∩ AcuteTreatmentSummary • s.drug = m.drug ∧ s.formulationScope = allFormulations ∧ sameSpan(s.period, c.timeRange)) ∧
     (∃ s ∈ parts(o) ∩ AcuteTreatmentSummary • s.drug = m.drug ∧ s.formulationScope = singleFormulation ∧
        s.formulations = {m.formulation} ∧ sameSpan(s.period, c.timeRange))) ∧
  (∀ t ∈ c.subject.preventiveTreatments • startOf(c, t) ≠ ∅ ⇒
     ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views; rc ∈ v.content ∩ ResponseComparison • rc.treatment = t ∧
       ∀ p ∈ {rc.baseline} ∪ ran rc.onTreatment • ∃ s ∈ v.content ∩ AcuteTreatmentSummary • s.drug = m.drug ∧ s.period = p)
```
- Reading: For each acute medication, its effectiveness across the attacks treated with it is available for the selected time range, for all its formulations and separately for each formulation; and for each preventive treatment that has started, it is available separately for the pre-treatment baseline period and each on-treatment period, next to the response comparison.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-021, OUT-023
- Evidence: Stage 1 OUT-023.

### INV-072 Acute-treatment summary content
- Predicate:
```omn
∀ s : AcuteTreatmentSummary • (∀ k ∈ requiredOutcomes(s.earlyTimePoint) • ∃ os ∈ s.outcomes • os.measure = k) ∧
  #s.sequence = s.treatedAttacks ∧
  (∀ l ∈ ran s.sequence • l.intakeTiming ≠ ∅ ∧
     ∀ k ∈ requiredOutcomes(s.earlyTimePoint) • ∃ b : 𝔹 • AttackOutcomeResult(measure ↦ k, achieved ↦ b) ∈ l.results)
```
- Reading: An acute-treatment summary shows every outcome measure of its time point (pain freedom, absence of the most bothersome symptom, headache relief and non-pain-symptom status at 2 hours or 15 minutes; sustained pain freedom, maintained relief and maintained non-pain-symptom status to 24 hours; rescue or repeat medication; relapse; drug-related adverse events and whether they were regarded as meaningful). It lists every treated attack it summarises, in order, and each attack line shows the result of every one of these outcome measures (so the absence of the most bothersome symptom is shown for each treated attack) and when the medication was taken relative to onset or the pain intensity at intake. The consistency of effect across consecutive treated attacks is thus visible.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-012, OUT-023, OUT-031
- Evidence: Stage 1 OUT-012 ("both across periods and in the response of individual treated attacks (see OUT-023)"), OUT-023 ("SHOULD show how consistently the drug was effective across consecutive treated attacks"), OUT-031.

### INV-073 Early time point: 15 minutes for cluster headache, otherwise 2 hours
- Predicate:
```omn
∀ s : AcuteTreatmentSummary • (concerns(ctx, s.typeScope, c3_1) ⇒ s.earlyTimePoint = fifteenMinutes) ∧
  (¬ concerns(ctx, s.typeScope, c3_1) ⇒ s.earlyTimePoint = twoHours)
```
- Reading: Summaries of treated cluster-headache attacks use the 15-minute time point; all others use 2 hours.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-023, OUT-031
- Evidence: Stage 1 OUT-023 ("For cluster headache, the corresponding time point is 15 minutes"), OUT-031.

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
      (s.formulationScope = singleFormulation ⇒ ∀ f ∈ l.formulation • f ∈ s.formulations)) ∧
   (s.formulationScope = singleFormulation ⇒ #s.formulations ≤ 1))
```
- Reading: For each outcome, the attacks with the outcome do not exceed the attacks for which it is shown, which do not exceed the attacks the summary covers; a proportion is the one divided by the other; the time point of the outcome is the summary's; when the summary lists all its attacks, its counts are those of its lines. A summary lists its attacks in order, once each, all of its drug and period (and formulation), and has one outcome summary per measure.
- Conformance: definitional (E-051, E-052). Scope: output.
- Realises: OUT-023
- Evidence: Stage 1 OUT-023.

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

### INV-076 Associated symptoms in the response of treated attacks, for migraine
- Predicate:
```omn
∀ l : TreatedAttackLine • hasType(ctx, c1) ⇒ ∀ a : AssociatedSymptom • ∃ st ∈ l.symptomStatus • st.symptom = a
```
- Reading: For a subject with migraine, each treated-attack line shows whether nausea/vomiting, photophobia and phonophobia were present at the early time point.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-012
- Evidence: Stage 1 OUT-012 ("both across periods and in the response of individual treated attacks (see OUT-023)").
- Notes: "For migraine" is the subject condition `hasType(ctx, c1)` for both parts of OUT-012, here and across periods (INV-022), and it is the condition of `symptomStatus` (E-053). A subject with migraine may also have another headache type (OUT-029); the treated-attack lines are not assigned to headache types, because such an assignment would be a derivation from input (section 1, item 3), so every treated-attack line of a subject with migraine shows the three statuses.

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
    (∀ l ∈ ran g.lines • l.role = g.role ∧ drugClassOf(l.drug) = g.drugClass) ∧
    (∀ i ∈ dom g.lines • i < #g.lines ⇒ ∀ a ∈ g.lines(i).startDate; b ∈ g.lines(i + 1).startDate • a ≤ b) ∧
    (∀ l ∈ ran g.lines; g₂ ∈ ran v.preventiveGroups ∪ ran v.acuteGroups • l ∈ ran g₂.lines ⇒ g₂ = g)
```
- Reading: Preventive and acute treatments are listed separately; within each, treatments are grouped by drug class (one group per class), each treatment appears in one group, and within a group treatments are in order of their start dates.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-024
- Evidence: Stage 1 OUT-024 ("a chronological list [...] grouped by drug class").

### INV-079 Treatment lines agree with the treatment course
- Predicate:
```omn
∀ l : TreatmentLine • (l.role = preventive ⇔ l.treatment ∈ ctx.subject.preventiveTreatments) ∧
  (l.role = acute ⇔ l.treatment ∈ ctx.subject.acuteTreatments) ∧ l.drug = drugOf(l.treatment) ∧
  (∀ s ∈ l.startDate • eventOn(ctx, l.treatment, start, s)) ∧
  (∀ e ∈ l.stopDate • ∃ k : StopKind • eventOn(ctx, l.treatment, stop(k), e)) ∧
  (∀ s ∈ l.startDate; e ∈ l.stopDate • s ≤ e ∧ ∀ d ∈ l.duration • d = daysLong(days(s, e))) ∧
  (¬ stopped(ctx, l.treatment) ⇒ ∀ s ∈ l.startDate; d ∈ l.duration • s ≤ ctx.asOf ∧ d = daysLong(days(s, ctx.asOf))) ∧
  (∀ dc ∈ l.doseChanges • eventOn(ctx, l.treatment, doseChange(dc.direction), dc.date)) ∧
  (∀ r ∈ l.preventiveResponse • r.treatment = l.treatment) ∧ (∀ a ∈ l.adherence • a.treatment = l.treatment) ∧
  (∀ s ∈ l.acuteResponse • s.drug = l.drug)
```
- Reading: A treatment line shows the subject's treatment: its start, stop and dose changes on the dates they occurred, a stop date not before the start date, a duration equal to the days from start to stop or, for a treatment that has not stopped, from start to the as-of date of the output (its duration to date), and the response summary and adherence of the same treatment.
- Conformance: definitional (E-055). Scope: output.
- Realises: OUT-024, OUT-039
- Evidence: Stage 1 OUT-024 ("start and stop dates, dose changes, treatment duration").
- Notes: A treatment that has not stopped has no stop event on or before the as-of date, and its start lies on or before that date (INV-001), so `days(s, ctx.asOf)` is defined. `days` counts both the first and the last day (section 2.8), as for a stopped treatment.

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

### 6.9 Instruments

### INV-081 Results of validated instruments where available
- Predicate:
```omn
∀ c ∈ Ctx; a ∈ c.subject.instrumentAdministrations • inSpan(a.date, c.timeRange) ⇒
  ∃ o : Output • (c, o) ∈ Rep ∧ ∃ r ∈ parts(o) ∩ InstrumentResult • r.instrument = a.instrument ∧ r.completionDate = {a.date} ∧
    ((∃ b ∈ c.subject.instrumentAdministrations • b.instrument = a.instrument ∧ b.date < a.date) ⇒ r.baselineResult ≠ ∅)
```
- Reading: Every available instrument result in the selected time range is reported, and, where an earlier administration of the same instrument exists, with the change from the baseline administration.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-026
- Evidence: Stage 1 OUT-026.

### INV-082 Instrument results agree with the instrument's published value set
- Predicate:
```omn
∀ r : InstrumentResult •
  (r.instrument ∈ dom scoreRange ⇒ ∀ x ∈ r.totalScore • x ≥ scoreRange(r.instrument).low ∧ ∀ h ∈ scoreRange(r.instrument).high • x ≤ h) ∧
  (r.instrument ∈ wholeNumberScores ⇒ ∀ x ∈ r.totalScore • x ∈ ℕ) ∧
  (∀ cat ∈ r.category • banded(r.instrument) ⇒ ∃ b ∈ gradeBands • cat = band(b) ∧ b.instrument = r.instrument ∧ ∀ x ∈ r.totalScore • inBand(x, b)) ∧
  (∀ cat ∈ r.category; b : GradeBand • cat = band(b) ⇒ b ∈ gradeBands ∧ b.instrument = r.instrument) ∧
  (r.instrument ∈ dom publishedRecall ⇒ ∀ rp ∈ r.recallPeriod • rp = publishedRecall(r.instrument)) ∧
  (∀ b ∈ r.baselineResult • b.instrument = r.instrument ∧ b ≠ r ∧ ∀ d₁ ∈ b.completionDate; d₂ ∈ r.completionDate • d₁ < d₂) ∧
  (∀ ch ∈ r.changeFromBaseline; b ∈ r.baselineResult; x ∈ r.totalScore; y ∈ b.totalScore • ch = x − y) ∧
  (∀ d ∈ r.completionDate • InstrumentAdministration(instrument ↦ r.instrument, date ↦ d) ∈ ctx.subject.instrumentAdministrations)
```
- Reading: A total score lies in the instrument's score range (36–78 for HIT-6; at least 0 for MIDAS, PedMIDAS and HALT, for which the model states no upper bound) and is a whole number for HIT-6, MIDAS, PedMIDAS, HALT-90 and HALT-30; the grade or category shown is a published band of that instrument that contains the score; the recall period shown is the instrument's published recall period (3 months for MIDAS, PedMIDAS and HALT-90, 1 month for HIT-6 and HALT-30); the baseline administration is an earlier result of the same instrument; the change from baseline is the score minus the baseline score; the completion date is that of an available result.
- Conformance: definitional (E-057, E-058). Scope: output.
- Realises: OUT-026, OUT-036
- Evidence: Stage 1 OUT-026, OUT-036; [S-101], [S-102], [S-103], [S-014] quoted in E-057.

### INV-083 Screening results next to the headache outputs
- Predicate:
```omn
∀ c ∈ Ctx; a ∈ c.subject.screeningAdministrations • inSpan(a.date, c.timeRange) ⇒
  ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views; r ∈ v.content ∩ ScreeningResult •
    r.instrument = a.instrument ∧ r.date = {a.date} ∧ r.scores ≠ ∅ ∧ ∃ m ∈ v.content ∩ HeadacheDays • m.typeScope = allTypes
```
- Reading: Every available depression or anxiety screening result in the selected time range is reported with instrument name, date and score, in a view that also shows headache outputs.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-033
- Evidence: Stage 1 OUT-033.

### INV-084 Screening results are not psychiatric diagnoses
- Predicate:
```omn
¬ ∃ r : ScreeningResult; x : Text • diagnosis(psychiatricDiagnosis(x)) ∈ r.claims ∨
  (∃ a : Annotation • r ∈ a.qualifies ∧ diagnosis(psychiatricDiagnosis(x)) ∈ a.claims)
```
- Reading: A screening result, or a label qualifying it, is not presented as a psychiatric diagnosis.
- Conformance: SHOULD NOT. Scope: output.
- Realises: OUT-033, OUT-038
- Evidence: Stage 1 OUT-033 Caveats ("The output therefore reports scores as screening results, not as psychiatric diagnoses (see OUT-038)"), OUT-038.

### INV-085 Screening scores lie in the instrument's range
- Predicate:
```omn
∀ r : ScreeningResult • (∀ s₁, s₂ ∈ r.scores • s₁.subscale = s₂.subscale ⇒ s₁ = s₂) ∧
  (r.instrument = hads ⇒ ∀ s ∈ r.scores • s.subscale ∈ {anxietySubscale, depressionSubscale} ∧ s.score ≤ 21) ∧
  (r.instrument = phq9 ⇒ ∀ s ∈ r.scores • s.subscale = wholeScale ∧ s.score ≤ 27) ∧
  (r.instrument = gad7 ⇒ ∀ s ∈ r.scores • s.subscale = wholeScale ∧ s.score ≤ 21) ∧
  (∀ d ∈ r.date • ScreeningAdministration(instrument ↦ r.instrument, date ↦ d) ∈ ctx.subject.screeningAdministrations)
```
- Reading: HADS shows anxiety and depression subscale scores of 0 to 21; PHQ-9 a total of 0 to 27; GAD-7 a total of 0 to 21; each subscale once; the date is that of an available result.
- Conformance: definitional (E-059). Scope: output.
- Realises: OUT-033
- Evidence: Stage 1 OUT-033; [S-104], [S-105] quoted in E-059.

### 6.10 Special populations and classification support

### INV-086 Menstrual-relation view for patients who menstruate
- Predicate:
```omn
∀ c ∈ Ctx • c.subject.menstruates ⇒ ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ MenstrualRelationView • sameSpan(v.covers, c.timeRange)
```
- Reading: For patients who menstruate, the diary can show migraine attacks and migraine days in relation to menstruation across consecutive cycles for the selected time range, with the perimenstrual window and the number of complete cycles.
- Conformance: MUST. Scope: repertoire.
- Realises: OUT-030
- Evidence: Stage 1 OUT-030.

### INV-087 Menstrual cycles, the perimenstrual window and attacks
- Predicate:
```omn
(∀ cl : CycleLine •
   (¬ cl.complete ⇒ cl.cycle.to = viewOf(cl).covers.end) ∧
   cl.firstDayOfMenstruation = cl.cycle.from ∧ cl.firstDayOfMenstruation = min cl.menstruationDays ∧
   (∀ d ∈ cl.menstruationDays • inSpan(d, cl.cycle)) ∧ (∀ d ∈ cl.migraineDays • inSpan(d, cl.cycle)) ∧
   cl.perimenstrualWindow = DateSpan(from ↦ plusDays(cl.firstDayOfMenstruation, − windowDaysBefore),
                                     to ↦ plusDays(cl.firstDayOfMenstruation, windowDaysAfter)) ∧
   ∀ a ∈ cl.attacks • a ∈ viewOf(cl).content ∧ inSpan(a.onset, cl.cycle)) ∧
(∀ a : AttackMark • a.inPerimenstrualWindow ⇔ ∃ cl ∈ viewOf(a).content ∩ CycleLine • inSpan(a.onset, cl.perimenstrualWindow)) ∧
(∀ v : MenstrualRelationView • ran v.cycles ⊆ v.content ∧
   v.completeCycles = #{cl ∈ ran v.cycles | cl.complete ∧ v.covers.start ≤ cl.cycle.from ∧ cl.cycle.to ≤ v.covers.end} ∧
   (∀ i ∈ dom v.cycles • i < #v.cycles ⇒ v.cycles(i).complete ∧ v.cycles(i + 1).cycle.from = next(v.cycles(i).cycle.to)) ∧
   (∀ a ∈ v.content ∩ AttackMark • ∃₁ cl ∈ ran v.cycles • a ∈ cl.attacks) ∧
   (∀ cl ∈ ran v.cycles • cl.cycle.from ≤ v.covers.end ∧ v.covers.start ≤ cl.cycle.to))
```
- Reading: Every cycle line, in whichever view it is shown, begins on its first day of menstruation (day 1), shows its menstruation days and migraine days within the cycle, and, if the cycle has not ended, is shown to the last day of the period its view covers. The perimenstrual window of a cycle runs from 2 days before to 2 days after day 1 (days −2 to +3, there being no day 0). The attacks of a cycle are shown in the same view and lie in the cycle, and an attack mark is marked as in the window exactly when its onset falls in the perimenstrual window of a cycle shown in the same view. The menstrual-relation view shows, as its own items, consecutive cycles that overlap its period; every cycle except the last has ended; every attack it shows belongs to one cycle; the number of complete cycles stated is the number of cycles shown that have ended and lie wholly within the period the view covers.
- Conformance: definitional (E-060, E-061). Scope: output.
- Realises: OUT-030, OUT-035
- Evidence: Stage 1 OUT-030; OUT-035 ("where relevant, the relationship to menstruation"); [S-001] A1.1 quoted in E-060.
- Notes: A window of a cycle can begin in the previous cycle (days −2 and −1), so attacks are matched against the windows of all cycles shown in the view. The relations of the derived attributes (`firstDayOfMenstruation`, `perimenstrualWindow`, `inPerimenstrualWindow`) hold for every cycle line and attack mark, including those of the patient-facing overview (INV-105); the structure of a sequence of cycles and `completeCycles` belong to the menstrual-relation view.

### INV-088 Cluster-headache view
- Predicate:
```omn
∀ c ∈ Ctx • hasType(c, c3_1) ⇒ ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ ClusterView • sameSpan(v.covers, c.timeRange) ∧
  (∀ b ∈ ran v.bouts; k : RateBasis • (∀ s ∈ b.start • s ≤ v.covers.end) ∧ (∀ e ∈ lastDay(b) • v.covers.start ≤ e) ⇒
     ∃ r ∈ v.rates • r.bout = b ∧ r.basis = k) ∧
  (∀ m ∈ c.subject.acuteMedications • ∃ s ∈ v.acute • s.drug = m.drug ∧ s.earlyTimePoint = fifteenMinutes ∧
     ∃ os ∈ s.outcomes • os.measure = rescueOrRepeatMedication)
```
- Reading: For patients with cluster headache, a view is available that shows cluster periods (including previous bouts) and remission periods, attacks per day and per week for every active period within the selected time range, and, for each acute medication, effectiveness at 15 minutes and the need for rescue treatment.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-031
- Evidence: Stage 1 OUT-031.

### INV-089 Cluster periods, remissions and rates are consistent
- Predicate:
```omn
(∀ x : ClusterPhaseItem • (x.ongoing ⇒ x.end = ∅) ∧
   (∀ s ∈ x.start; e ∈ lastDay(x) • s ≤ e ∧ ∀ d ∈ x.duration • d = daysLong(days(s, e))) ∧
   (x ∈ RemissionPeriodItem ⇒ ∀ s ∈ x.start; e ∈ lastDay(x) • plusMonths(s, remissionMoreThanMonths) ≤ e)) ∧
(∀ v : ClusterView • (∀ i ∈ dom v.bouts • i < #v.bouts ⇒ ¬ v.bouts(i).ongoing ∧
      ∀ e ∈ v.bouts(i).end; s ∈ v.bouts(i + 1).start • e < s) ∧
   (∀ i ∈ dom v.remissions • i < #v.remissions ⇒ ¬ v.remissions(i).ongoing ∧
      ∀ e ∈ v.remissions(i).end; s ∈ v.remissions(i + 1).start • e < s) ∧
   (∀ b ∈ ran v.bouts; r ∈ ran v.remissions • ∀ bs ∈ b.start; be ∈ lastDay(b); rs ∈ r.start; re ∈ lastDay(r) • be < rs ∨ re < bs)) ∧
(∀ r : ClusterAttackRate • r.rate ≥ 0 ∧ (∀ s ∈ r.bout.start • s ≤ r.period.start) ∧ (∀ e ∈ lastDay(r.bout) • r.period.end ≤ e))
```
- Reading: An ongoing period has no end date yet; a duration is the number of days from start to end (or to the end of the covered period while ongoing); a remission period lasts more than three months; bouts and remissions are each in chronological order, only the last can be ongoing, and no bout overlaps a remission; an attack rate refers to a period within its bout.
- Conformance: definitional (E-063, E-064). Scope: output.
- Realises: OUT-031
- Evidence: Stage 1 OUT-031 ("using the ICHD-3 definitions"); [S-001] remission duration quoted in E-063.

### INV-090 Caveats of the trigger co-occurrence view
- Predicate:
```omn
∀ v : TriggerCooccurrenceView • annotated(v, coOccurrenceNotCausation) ∧ annotated(v, apparentTriggersMayBePremonitorySymptoms)
```
- Reading: A trigger view states that it shows co-occurrence and not causation, and that some apparent triggers are early (premonitory) symptoms of the attack.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-032
- Evidence: Stage 1 OUT-032 ("Strength: MAY (caveats SHOULD)").

### INV-091 No composite index as a primary measure for migraine
- Predicate:
```omn
¬ ∃ x : CompositeIndex • concerns(ctx, x.typeScope, c1) ∧ x.role = primaryRole
```
- Reading: For migraine, no composite headache index is presented as a primary measure.
- Conformance: SHOULD NOT. Scope: output.
- Realises: OUT-037
- Evidence: Stage 1 OUT-037.

### INV-092 A migraine composite index is exploratory and shown with its components
- Predicate:
```omn
∀ x : CompositeIndex • concerns(ctx, x.typeScope, c1) ⇒ annotated(x, exploratoryMeasure) ∧
  (∀ m ∈ x.components • m ∈ viewOf(x).content ∧ m.period = x.period ∧ m.typeScope = x.typeScope) ∧
  ∀ d ∈ x.combines • ∃ m ∈ x.components • dimensionOf(m, d)
```
- Reading: If a composite index is shown for migraine, it is labelled exploratory and shown, in the same view and for the same period, with a component measure for each dimension it combines.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-037
- Evidence: Stage 1 OUT-037.

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
  (∀ d ∈ c.previousConsultation • ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ ClinicianSummary •
     v.covers.start = d ∧ v.covers.end = c.asOf)
```
- Reading: For a clinician reader (the treating clinician with whom the summary is shared), a clinician-facing summary is available for the period chosen by the clinician and for the period since the previous consultation.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-034
- Evidence: Stage 1 OUT-034.

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
∀ c ∈ Ctx • c.subject.ageGroup = childOrAdolescent ⇒
  (∀ a ∈ c.subject.instrumentAdministrations • a.instrument = pedmidas ∧ inSpan(a.date, c.timeRange) ⇒
     ∃ o : Output • (c, o) ∈ Rep ∧ ∃ r ∈ parts(o) ∩ InstrumentResult • r.instrument = pedmidas ∧ r.completionDate = {a.date} ∧
       r.recallPeriod = {recallMonths(3)}) ∧
  (∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views; sr ∈ v.content ∩ Series • tiles(sr, c.timeRange, c.granularity) ∧
     (perPeriod(v, sr, fiDays(paidWorkOrSchool, affected), allTypes) ∨
      (perPeriod(v, sr, fiDays(paidWorkOrSchool, missed), allTypes) ∧ perPeriod(v, sr, fiDays(paidWorkOrSchool, impaired), allTypes))) ∧
     perPeriod(v, sr, CaregiverImpact, allTypes))
```
- Reading: For children and adolescents, available PedMIDAS results are reported with their 3-month recall period, and school days missed or impaired and the impact on parents or caregivers are reported for every period of the selected time range.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-036
- Evidence: Stage 1 OUT-036 (a), (b).
- Notes: PedMIDAS results can be reported only where they exist; the condition is that of OUT-026 ("Where results of validated instruments are available").

### INV-097 Paediatric comparisons use periods of equal length
- Predicate:
```omn
ctx.subject.ageGroup = childOrAdolescent ⇒
  (∀ pc : PeriodComparison • equalLengths(ran pc.periods)) ∧ (∀ rc : ResponseComparison • equalLengths({rc.baseline} ∪ ran rc.onTreatment))
```
- Reading: For children and adolescents, the periods compared in one comparison have equal length.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-036
- Evidence: Stage 1 OUT-036 (c) ("apply equal-length period comparisons as in OUT-001").

### INV-098 Paediatric outputs are presented as supportive information
- Predicate:
```omn
ctx.subject.ageGroup = childOrAdolescent ⇒ ∀ v : View • annotated(v, supportiveInformation)
```
- Reading: For children and adolescents, every view is presented as supportive information.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-036
- Evidence: Stage 1 OUT-036 Caveats ("Paediatric outputs should therefore be presented as supportive information").

### INV-099 Interpretive caveats on every summary
- Predicate:
```omn
∀ v : View • annotated(v, patientReportedDiaryInformation) ∧ annotated(v, supportsDoesNotReplaceClinicalAssessment)
```
- Reading: Every summary output states that it summarises patient-reported diary information and that it supports but does not replace clinical assessment and diagnosis.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-038
- Evidence: Stage 1 OUT-038.

### INV-100 Indicators, labels and associations require clinical interpretation
- Predicate:
```omn
(∀ i : MedicationOveruseIndicator • annotated(i, requiresClinicalInterpretation)) ∧
(∀ L : ResponderLabel • annotated(L, requiresClinicalInterpretation)) ∧
(∀ v : TriggerCooccurrenceView • annotated(v, requiresClinicalInterpretation))
```
- Reading: The medication-overuse indicator, responder labels and trigger associations each state that they require clinical interpretation.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-016, OUT-020, OUT-032, OUT-038
- Evidence: Stage 1 OUT-038.

### INV-101 No output presented as replacing clinical assessment or as a diagnosis
- Predicate:
```omn
¬ ∃ x : Element • replacesClinicalAssessment ∈ x.claims ∨ ∃ d : DiagnosisRef • diagnosis(d) ∈ x.claims
```
- Reading: No element presents itself as replacing clinical assessment, or presents the subject as having a diagnosis.
- Conformance: SHOULD NOT. Scope: output.
- Realises: OUT-038
- Evidence: Stage 1 OUT-038 ("they support but do not replace clinical assessment and diagnosis").
- Notes: The negative counterpart of the caveat of INV-099: an output that carried the caveat and at the same time claimed to replace clinical assessment or to make a diagnosis would contradict itself. INV-043 (SHOULD NOT, OUT-028), INV-048 (MUST NOT, OUT-016) and INV-084 (SHOULD NOT, OUT-033) state the same prohibition for particular outputs, INV-048 at the stronger level that OUT-016 requires; they are consistent with this general one. INV-106 (MUST NOT, OUT-018) and INV-107 (SHOULD NOT, OUT-023) prohibit two particular decisions that Stage 1 leaves to the reader.

### INV-102 Treatment review view available for each preventive treatment
- Predicate:
```omn
∀ c ∈ Ctx; t ∈ c.subject.preventiveTreatments • startOf(c, t) ≠ ∅ ⇒
  ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ TreatmentReviewView • v.treatment = t
```
- Reading: For each preventive treatment that has started, a treatment review view is available.
- Conformance: MUST. Scope: repertoire.
- Realises: OUT-021
- Evidence: Stage 1 OUT-021.

### INV-103 Post-stop monitoring available after a stop, pause or reduction
- Predicate:
```omn
∀ c ∈ Ctx; e ∈ c.subject.courseEvents • e.treatment ∈ c.subject.preventiveTreatments ∧ startOf(c, e.treatment) ≠ ∅ ∧
  (e.kind is stop ∨ e.kind = doseChange(reduction)) ⇒
    ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ PostStopMonitoringView • v.treatment = e.treatment ∧ v.event = e.kind ∧ v.eventDate = e.date
```
- Reading: After each stop, pause or dose reduction of a preventive treatment, the post-stop monitoring view is available.
- Conformance: SHOULD. Scope: repertoire.
- Realises: OUT-022
- Evidence: Stage 1 OUT-022.

### INV-104 Clinician-facing summary content
- Predicate:
```omn
∀ v : ClinicianSummary • concise ∈ v.qualities ∧
  shownDay(v, headacheDays, v.covers, allTypes) ∧ (hasType(ctx, c1) ⇒ shownDay(v, migraineDays, v.covers, allTypes)) ∧
  shownDay(v, moderateSevereHeadacheDays, v.covers, allTypes) ∧ (∃ e ∈ v.content ∩ AttackCount • e.period = v.covers ∧ e.typeScope = allTypes) ∧
  shownDay(v, headacheFreeDays, v.covers, allTypes) ∧ shownDay(v, symptomFreeDays, v.covers, allTypes) ∧
  (0 ∈ daysOf(v, migraineDays, v.covers, allTypes) ⇒
     ∃ mk ∈ v.content ∩ MigraineFreePeriodMark • mk.period = v.covers ∧ mk.typeScope = allTypes) ∧
  ((∃ g : Granularity • containsPeriodOf(spanOf(v.covers), g)) ⇒
   ∃ sr ∈ v.content ∩ Series • within(first(sr.periods), v.covers) ∧ within(last(sr.periods), v.covers) ∧
     perPeriod(v, sr, HeadacheDays, allTypes) ∧ (hasType(ctx, c1) ⇒ perPeriod(v, sr, MigraineDays, allTypes)) ∧
     perPeriod(v, sr, ModerateSevereHeadacheDays, allTypes) ∧ perPeriod(v, sr, AttackCount, allTypes) ∧
     (∀ p ∈ ran sr.periods • 0 ∈ daysOf(v, migraineDays, p, allTypes) ⇒
        ∃ mk ∈ v.content ∩ MigraineFreePeriodMark • mk.period = p ∧ mk.typeScope = allTypes) ∧
     (sr.granularity ∈ MonthlyKind ⇒ ∀ p ∈ ran sr.periods •
        ∀ s ∈ {m ∈ ctx.subject.acuteMedications • ofClassUse(classOf(m.drug))} ∪ {combinedUse} •
          ∃ i ∈ v.content ∩ MedicationOveruseIndicator • i.period = p ∧ i.scope = s)) ∧
  (∀ e ∈ ctx.subject.courseEvents • e.treatment ∈ ctx.subject.preventiveTreatments ∧ markedKind(e.kind) ∧ inPeriod(e.date, v.covers) ⇒
     ∃ mk ∈ v.content ∩ TreatmentMarker • mk.treatment = e.treatment ∧ mk.event = e.kind ∧ mk.date = e.date) ∧
  shownDay(v, acuteMedicationDays(allAcuteMedication), v.covers, allTypes) ∧
  (∀ m ∈ ctx.subject.acuteMedications • shownDay(v, acuteMedicationDays(ofClass(classOf(m.drug))), v.covers, allTypes) ∧
     shownDay(v, acuteMedicationDays(ofDrug(m.drug)), v.covers, allTypes)) ∧
  (∃ sr ∈ v.content ∩ Series • sr.granularity = calendarWeek ∧ perPeriod(v, sr, TotalAcuteMedicationDays, allTypes)) ∧
  (∀ t ∈ ctx.subject.preventiveTreatments • startOf(ctx, t) ≠ ∅ ⇒
     (∃ rc ∈ v.content ∩ ResponseComparison • rc.treatment = t) ∧ (∃ a ∈ v.content ∩ AdherenceSummary • a.treatment = t)) ∧
  (∀ m ∈ ctx.subject.acuteMedications • ∃ s ∈ v.content ∩ AcuteTreatmentSummary • s.drug = m.drug) ∧
  (∀ t ∈ ctx.subject.preventiveTreatments ∪ ctx.subject.acuteTreatments • ∃ l ∈ v.content ∩ TreatmentLine • l.treatment = t) ∧
  (∀ a ∈ ctx.subject.instrumentAdministrations • inPeriod(a.date, v.covers) ⇒
     ∃ r ∈ v.content ∩ InstrumentResult • r.instrument = a.instrument ∧ r.completionDate = {a.date}) ∧
  (∀ d ∈ {paidWorkOrSchool, householdWork, socialOrLeisure} • ∃ m ∈ v.content ∩ fiDays(d, affected) • m.period = v.covers) ∧
  (∃ m ∈ v.content ∩ DayCount • m.period = v.covers ∧ ∃ d : ImpactDomain • m.measure = functionalImpactDays((d, severelyImpaired)))
```
- Reading: The clinician-facing summary is concise and brings together, for the period it covers: the frequency measures (headache, migraine, moderate/severe, headache-free and symptom-free days, attacks, and the marks of periods without migraine days) and, when the covered period contains at least one whole calendar month, 28-day period or calendar week, their time course (headache days, migraine days, moderate/severe headache days and attacks for every period of a series within the covered period) with treatment markers; acute-medication days in total, by class, by drug and per week, and the medication-overuse indicators of its monthly periods; the response comparison and adherence of each preventive treatment, the effectiveness of each acute medication, and the treatment history; the available instrument results; and functional impact (days affected in each of the three domains and days with severe functional impairment). Completeness accompanies its periods by INV-011.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-034, OUT-039
- Evidence: Stage 1 OUT-034 ("frequency measures and their time course (OUT-004 to OUT-009)", "functional impact (OUT-027)"), OUT-009 ("frequency measures (OUT-004 to OUT-007) as a time series of consecutive reporting periods"), OUT-027 ("including days with severe functional impairment"), OUT-039 ("The adherence output SHOULD also be available [...] in the clinician-facing summary (OUT-034)").
- Notes: Headache-free days, symptom-free days and the marks of periods without migraine days are included because OUT-034 names "frequency measures [...] (OUT-004 to OUT-009)", which includes OUT-008; see ISS-04. The covered period and each period of the series are marked as without migraine days where the summary shows 0 migraine days for them. Migraine days themselves, for the covered period and in the time course, are required for patients with migraine, the OUT-005 condition that OUT-034 keeps by its reference to OUT-005 (section 3.5), as in INV-035. A time course consists of whole periods of one granularity (E-006, INV-004). The period since the previous consultation may be shorter than a week, or contain no whole calendar week (INV-094 admits any previous-consultation date up to the as-of date); such a period has no time course of its own, so the series, with the marks and medication-overuse indicators of its periods, is required only when the covered period contains at least one whole period (`containsPeriodOf`, E-006). Every other component applies to any covered period, including the mark of the covered period itself and the treatment markers for every event within it.

### INV-105 Patient-facing overview content
- Predicate:
```omn
∀ v : PatientOverview • plainLanguage ∈ v.qualities ∧
  (∃ sr ∈ v.content ∩ Series • tiles(sr, spanOf(v.covers), sr.granularity) ∧
     perPeriod(v, sr, HeadacheDays, allTypes) ∧ perPeriod(v, sr, MigraineDays, allTypes) ∧
     perPeriod(v, sr, IntensitySummary, allTypes) ∧ perPeriod(v, sr, TotalAcuteMedicationDays, allTypes)) ∧
  ((∃ t ∈ ctx.subject.preventiveTreatments • startOf(ctx, t) ≠ ∅) ∨ ctx.subject.acuteMedications ≠ ∅ ⇒
     ∃ x ∈ v.content • x ∈ ResponseComparison ∪ AcuteTreatmentSummary) ∧
  (ctx.subject.menstruates ⇒ ∃ cl ∈ v.content ∩ CycleLine • cl.cycle.from ≤ v.covers.end ∧ v.covers.start ≤ cl.cycle.to)
```
- Reading: The patient-facing overview, in plain language, shows the patient's headache pattern over time (headache days, migraine days, intensity and acute-medication days for every period of a series spanning its period), the effect of the patient's treatment where the patient has a preventive treatment that has started or uses acute medication, and, for patients who menstruate, the relationship to menstruation: a menstrual cycle that overlaps the period the overview covers.
- Conformance: SHOULD. Scope: output.
- Realises: OUT-035
- Evidence: Stage 1 OUT-035.
- Notes: Migraine days are included as OUT-035 names them, without the OUT-005 condition; see ISS-03. A period need not contain the first day of a menstruation (for example a single calendar week), so the cycle line is required to overlap the covered period, as the cycles of the menstrual-relation view do (INV-087), not to begin in it; INV-087 also defines the cycle line in this view. The effect of a preventive treatment is shown by a response comparison, which exists only for a treatment that has started (INV-056).

### 6.12 Decisions left to the reader

### INV-106 No output decides on the continuation of a preventive treatment
- Predicate:
```omn
¬ ∃ x : Element • continuationDecision ∈ x.claims
```
- Reading: No element presents a decision to continue, stop or change a preventive treatment. The output shows the change from baseline and, where it shows a responder label, the criterion that a reader chooses to apply, and it leaves the decision to the reader.
- Conformance: MUST NOT. Scope: output.
- Realises: OUT-018, OUT-020
- Evidence: Stage 1 OUT-018 Caveats ("the output shows the change and names the criterion a reader chooses to apply (OUT-020), but does not itself decide on continuation"); OUT-020 Rationale ("Showing the named criterion with the underlying values serves both positions without the output itself making the decision").
- Notes: The level is MUST NOT because the prohibition is the negative form of a Caveat of OUT-018, whose strength is MUST (section 3.3, item 6); OUT-020 (SHOULD) states the same in its Rationale and is the second part cited. A responder or control-level label (E-046) classifies the response under a named criterion; it is not a continuation decision, so this invariant does not restrict the labels that OUT-020 permits.

### INV-107 No output decides which definition of acute treatment response applies
- Predicate:
```omn
¬ ∃ x : Element • acuteResponseDefinitionDecision ∈ x.claims
```
- Reading: No element presents one definition of acute treatment response (for example pain freedom at 2 hours, or the EHF definition of effective attack treatment) as the one that applies. The output shows pain freedom and headache relief side by side and leaves the choice of definition to the reader.
- Conformance: SHOULD NOT. Scope: output.
- Realises: OUT-023
- Evidence: Stage 1 OUT-023 Caveats ("The output therefore shows headache relief next to pain freedom and does not itself decide which definition of response applies").
- Notes: The level is SHOULD NOT, the negative form of a Caveat of OUT-023, whose strength is SHOULD (section 3.3, item 6).

## 7. Traceability

Every Stage 1 requirement, in Stage 1 order (OUT-039 follows OUT-025), with the elements and invariants that realise it (from their Realises fields) and its coverage. Coverage is "full" when every observable property of the Statement, and every Caveat that constrains what an output shows, is represented.

| Requirement | Elements | Invariants | Coverage and reason |
|---|---|---|---|
| OUT-001 | E-002, E-003, E-005, E-006, E-007, E-012, E-015, E-016, E-037, E-043 | INV-001, INV-002, INV-003, INV-004, INV-005, INV-014, INV-015, INV-016, INV-017, INV-037, INV-038, INV-055 | full — every view states its reporting period with start, end and length (E-003, E-005, INV-002, INV-003); frequency outputs per calendar month or 28-day period (INV-014 to INV-017); comparison of selected equal-length periods and of baseline and on-treatment periods of equal length (INV-037, INV-055); the stated length makes the days of each calendar month visible (Caveat). |
| OUT-002 | E-011, E-015, E-016, E-017, E-019 | INV-008 | full — a definition label for each defined measure shown in a view (E-011, INV-008). |
| OUT-003 | E-001, E-013 | INV-011, INV-012, INV-013 | full — completeness indicator for each period, next to the summary measures, as covered days or proportion (E-013, INV-011, INV-012); no cut-off presented as validated (INV-013). |
| OUT-004 | E-006, E-007, E-011, E-014, E-015 | INV-001, INV-004, INV-005, INV-006, INV-009, INV-014 | full — per period for every period of the selected time range (INV-014), ICHD-3 definition (E-015, INV-009). |
| OUT-005 | E-008, E-009, E-011, E-014, E-016 | INV-005, INV-008, INV-015 | full — per period for patients with migraine (INV-015); definition label SHOULD (INV-008). |
| OUT-006 | E-011, E-014, E-017 | INV-005, INV-008, INV-016, INV-031 | full — per period (INV-016) with definition label (INV-008). |
| OUT-007 | E-011, E-019 | INV-006, INV-008, INV-010, INV-017 | full — separate element type (E-019), per period (INV-017), ICHD-3 definition label (INV-010). |
| OUT-008 | E-010, E-014, E-020, E-021, E-022 | INV-005, INV-031 | full — the three exploratory measures as MAY elements (E-020 to E-022), optional exploratory annotation (E-010), relations (INV-031). |
| OUT-009 | E-006, E-007, E-008, E-034, E-035 | INV-001, INV-004, INV-034, INV-035, INV-036 | full — time series of consecutive periods with markers for start, dose change and stop (E-034, E-035, INV-034 to INV-036); weekly values where weekly granularity is relevant (INV-034, INV-001). The purpose ("so that onset of effect [...] can be seen") is stated in the Meaning. |
| OUT-010 | E-023, E-037 | INV-018, INV-032, INV-039 | full — per period on a stated scale (E-023, INV-018), comparison between periods (INV-039; for children and adolescents between selected periods of equal length, as OUT-036 (c) requires), relations (INV-032). |
| OUT-011 | E-001, E-010, E-024 | INV-007, INV-019, INV-020, INV-021, INV-033 | full — per period (E-024, INV-019); label for treated attacks (INV-020); the Caveat as a SHOULD NOT (INV-021). |
| OUT-012 | E-008, E-009, E-025, E-026, E-050, E-051, E-053 | INV-022, INV-033, INV-072, INV-075, INV-076 | full — associated symptoms and most bothersome symptom across periods (E-025, E-026, INV-022) and in the response of individual treated attacks: every summarised attack is listed with the result of every outcome measure, including the absence of the most bothersome symptom (E-050, E-053, INV-072), and, for every subject with migraine as across periods, with the status of each associated symptom, once each (INV-075, INV-076). |
| OUT-013 | E-008, E-009, E-019, E-024, E-027 | — | full — aura count and duration as MAY elements for migraine with aura, separate from headache measures (E-027). |
| OUT-014 | E-009, E-014, E-028, E-029, E-032 | INV-001, INV-005, INV-023, INV-024 | full — total, per ICHD-3 8.2 class and per drug, together per period (E-028, E-029, INV-023), relations (INV-024). |
| OUT-015 | E-006, E-029, E-036 | INV-005, INV-025 | full — calendar-week view of acute-medication days in addition to per-period totals (E-036, INV-025). |
| OUT-016 | E-001, E-009, E-010, E-028, E-029, E-032 | INV-007, INV-024, INV-044, INV-045, INV-046, INV-047, INV-048, INV-100 | full — per period, per class and for 8.2.6 combined use, with ICHD-3 subtype, reference level and time span shown (E-032, INV-044 to INV-046); prompt wording (INV-047); not a diagnosis (INV-048); basis of 8.2.6 per ICHD-3 (ISS-01). Plain language for patients is in the Audience line only and is stated in the Meaning. |
| OUT-017 | E-008, E-010, E-039 | INV-007, INV-049, INV-050, INV-051, INV-052 | full — from the start of withdrawal, with the NICE 4–8-week window and continued over the following year (E-039, INV-049 to INV-051); worsening label (INV-052). |
| OUT-018 | E-001, E-008, E-040, E-041, E-042, E-043, E-045 | INV-001, INV-053, INV-054, INV-055, INV-056, INV-057, INV-058, INV-059, INV-106 | full — per preventive treatment, a baseline month and monthly on-treatment periods aligned to the start, so that monthly migraine days and monthly headache days are compared, with the values of each period and the absolute and percentage change (E-040, E-043, INV-053 to INV-057); evaluation time points of current guidance by treatment type, shown with the comparison, and a comparison of equal-length periods at every time point that has been reached and that a monthly on-treatment period can reach (E-041, E-042, INV-055, INV-058, INV-059), every preventive treatment having a guidance type and no course event preceding the treatment start (INV-001); the Caveat that the output does not itself decide on continuation (E-001, INV-106). The time points are those named in the Stage 1 evidence of OUT-018 (NICE CG150, AAN/AHS 2026, SIGN 155, EHF 2022, IHS 2024, NVN and the Russian clinical recommendations); see ISS-03 on migraine days. |
| OUT-019 | E-040, E-044 | INV-060, INV-061, INV-062 | full — residual migraine days and moderate/severe headache days per month next to every percentage change (E-044, INV-060, INV-061); see ISS-05. |
| OUT-020 | E-001, E-008, E-014, E-018, E-040, E-045, E-046, E-058 | INV-031, INV-054, INV-062, INV-063, INV-064, INV-065, INV-100, INV-106 | full — optional label (E-046) naming its criterion with thresholds (E-045, INV-062), with underlying values and, where they are available (OUT-026, OUT-023), the other values the criterion rests on (INV-062), consistent with the components of the criterion that the values shown decide, reduction components for a label over a single on-treatment period (INV-063, INV-064), not the sole indicator (INV-065); no automatic verdict on continuation (INV-106); see ISS-08. |
| OUT-021 | E-023, E-025, E-026, E-048, E-051, E-058 | INV-068, INV-069, INV-071, INV-102 | full — MUST components for the same periods: headache days, migraine days (for patients with migraine) and the acute-medication days of OUT-014 in total, per ICHD-3 8.2 class and per drug (E-048, INV-068, INV-102); SHOULD components where provided, including acute-treatment effectiveness per period and most recent instrument and PGIC results (INV-069, INV-071). The patient's own goals are brought by the reader (E-048 Notes). |
| OUT-022 | E-008, E-049 | INV-070, INV-103 | full — after stop, pause or reduction, headache and migraine days shown with the on-treatment period (whenever the event falls after the start day) and the original baseline (E-049, INV-070, INV-103); see ISS-03. |
| OUT-023 | E-001, E-008, E-050, E-051, E-052, E-053 | INV-069, INV-071, INV-072, INV-073, INV-074, INV-075, INV-107 | full — per acute medication and per formulation, all named outcome measures including relief, non-pain symptoms and adverse events, consistency across consecutive treated attacks (every summarised attack listed in order with the result of every outcome measure), timing of intake, 15 minutes for cluster headache, separate baseline and on-treatment summaries (E-050 to E-053, INV-071 to INV-075); the Caveat that the output does not itself decide which definition of response applies (E-001, INV-107). |
| OUT-024 | E-008, E-051, E-054, E-055 | INV-001, INV-077, INV-078, INV-079 | full — chronological lists of preventive and of acute treatments grouped by drug class with dates, dose changes, duration (to the stop, or to date for a treatment that has not stopped), response, adverse effects, stop reason and acute formulation (E-054, E-055, INV-077 to INV-079); start dates, durations and preventive response summaries wherever the treatment has a start, and no stop before the start (INV-001); Caveats stated in the Meaning. |
| OUT-025 | E-007, E-046, E-056, E-058 | INV-080 | full — MAY view for selected scheme windows labelled with the scheme name (E-056, INV-080). |
| OUT-039 | E-008, E-047, E-054, E-055, E-066 | INV-066, INV-067, INV-079, INV-104 | full — adherence next to the response comparison over the evaluation window (E-047, INV-066, INV-067), in the treatment history for every preventive treatment that has started (E-055) and in the clinician-facing summary (INV-104). |
| OUT-026 | E-008, E-057, E-058 | INV-081, INV-082 | full — results where available with name, date, recall, total score (in the instrument's range, a whole number for the instruments that have whole-number scores), published grading and change from baseline (E-057, E-058, INV-081, INV-082); see ISS-06. |
| OUT-027 | E-014, E-030, E-037 | INV-005, INV-026, INV-027, INV-033 | full — days affected per domain and days with severe impairment per period (E-030, INV-026), comparison of both with the baseline period (INV-027), relations (INV-033). |
| OUT-028 | E-001, E-006, E-009, E-011, E-038 | INV-008, INV-040, INV-041, INV-042, INV-043 | full — three most recent consecutive monthly periods with headache and migraine days (E-038, INV-040, INV-041); source definitions and codes SHOULD (INV-042); no diagnosis SHOULD NOT (INV-043); see ISS-03. |
| OUT-029 | E-008, E-009, E-012, E-023, E-029 | INV-001, INV-028, INV-029, INV-030 | full — frequency outputs and acute-medication days (total, per ICHD-3 8.2 class and per drug) per headache type and combined when more than one type is possible (INV-028), intensity per type where provided (INV-029), relations (INV-030); see ISS-09 on the weekly view and the overuse indicator. |
| OUT-030 | E-008, E-060, E-061 | INV-086, INV-087 | full — migraine attacks and days in relation to menstruation across consecutive cycles, ICHD-3 A1.1 window distinguished, number of complete cycles defined over the cycles shown (E-060, E-061, INV-086, INV-087); the relations of a cycle line and an attack mark hold in every view that shows them (INV-087). |
| OUT-031 | E-008, E-009, E-050, E-051, E-052, E-062, E-063, E-064 | INV-072, INV-073, INV-088, INV-089 | full — bouts and remissions with start, end and duration under the ICHD-3 definitions, attacks per day and per week in active periods, acute effectiveness at 15 minutes and rescue need, history of previous bouts as the chronological bout list (E-062 to E-064, INV-088, INV-089). |
| OUT-032 | E-010, E-065 | INV-007, INV-090, INV-100 | full — MAY view (E-065) with the two caveats SHOULD (INV-090) and the clinical-interpretation caveat (INV-100). |
| OUT-033 | E-001, E-008, E-059 | INV-083, INV-084, INV-085 | full — screening results where available with name, date and score next to headache outputs (E-059, INV-083, INV-085); not psychiatric diagnoses (INV-084). |
| OUT-034 | E-003, E-007, E-035, E-058, E-066 | INV-011, INV-094, INV-104 | full — concise clinician-facing summary for the chosen period and the period since the previous consultation, with all named components (E-066, INV-094, INV-104), including the time course of every frequency measure of OUT-004 to OUT-007 (whenever the covered period contains a whole period), the OUT-008 measures with periods without migraine days, and days with severe functional impairment; shareable represented by availability for clinician audiences; see ISS-04. |
| OUT-035 | E-003, E-007, E-023, E-035, E-060, E-067 | INV-087, INV-095, INV-105 | full — plain-language patient overview over time with the named components (E-067, INV-095, INV-105): treatment effect where a preventive treatment has started or acute medication is used, and, for patients who menstruate, a menstrual cycle that overlaps the covered period, defined as in the menstrual-relation view (INV-087); see ISS-03. |
| OUT-036 | E-007, E-008, E-010, E-030, E-031, E-037, E-043, E-057, E-058 | INV-033, INV-055, INV-082, INV-096, INV-097, INV-098 | full — (a) PedMIDAS with 3-month recall and (b) school days and caregiver impact (INV-096); (c) equal-length comparisons (INV-097); (d) efficacy from diary data by the response comparison, available for every subject (E-043, INV-055); supportive-information caveat (INV-098). |
| OUT-037 | E-008, E-009, E-010, E-012, E-033 | INV-007, INV-091, INV-092, INV-093 | full — for migraine no primary composite index (INV-091), exploratory label and components if shown (INV-092); AUC for tension-type headache with headache days (INV-093) (E-033). |
| OUT-038 | E-001, E-002, E-003, E-004, E-010, E-032, E-038, E-046, E-059, E-065 | INV-007, INV-043, INV-084, INV-099, INV-100, INV-101 | full — caveats on every view (INV-099); clinical-interpretation caveat on the overuse indicator, responder labels and trigger associations (INV-100); no output presented as replacing clinical assessment or as a diagnosis (INV-101). |

## 8. Stage 1 issues for the human

The model follows Stage 1 in each case below. Each issue is pointed to from the Notes of the elements it affects.

### ISS-01 The basis of the ICHD-3 8.2.6 indicator is not the total across all classes
- Stage 1: OUT-016 asks for the indicator "for ICHD-3 subtype 8.2.6, for the combined use of acute medication across classes (see the total across classes in OUT-014)". The total of OUT-014 is the total across all acute-medication classes, including combination analgesics and "other classes".
- Evidence: ICHD-3 8.2.6 criterion B counts a total over named classes only: [S-001] "Regular intake of any combination of ergotamine, triptans, non-opioid analgesics and/or opioids [...] on a total of ≥10 days/month for >3 months without overuse of any single drug or drug class alone." (8.2.6, diagnostic criterion B, p. 124). Medications of 8.2.8 ("medications other than those described above") are not among these classes.
- Effect on the model: so that the indicator relation is correct under ICHD-3 (Stage 2 PROCESS.md section 2), the basis of the 8.2.6 indicator is the days with any medication of the classes ICHD-3 names (`ofClasses(classesOf826)`, E-028, E-029, E-032), not the OUT-014 total. Whether days with combination-analgesic intake belong to that total is not stated explicitly by ICHD-3; the shown basis states the classes it covers.
- For the human: confirm that the 8.2.6 indicator rests on the classes named in ICHD-3 8.2.6 criterion B rather than on the OUT-014 total.

### ISS-02 "Simple analgesics" is not the ICHD-3 name of the class
- Stage 1: OUT-014 gives as an example of the ICHD-3 8.2 drug classes "ergotamine, triptans, simple analgesics, opioids, combination analgesics, and other classes".
- Evidence: ICHD-3 names this class non-opioid analgesics: [S-001] "8.2.3 Non-opioid analgesic-overuse headache" (classification list, p. 12) and "For the purposes of ICHD-3, all non-opioid analgesics are regarded as a single class" (8.2.3, comments, p. 123). In the downloaded ICHD-3 text, "simple analgesics" occurs only once, in an unrelated passage (on acute mountain sickness, section 10).
- Effect on the model: the class is named by its ICHD-3 subtype label (E-028). The example in OUT-014 is not a requirement, so the model is not narrowed.
- For the human: consider correcting the example label in Stage 1.

### ISS-03 Migraine days without the "patients with migraine" condition
- Stage 1: OUT-005 reports migraine days "for patients with migraine". OUT-018 ("monthly migraine days and monthly headache days"), OUT-022 ("headache and migraine frequency"), OUT-028 ("headache days and migraine days") and OUT-035 ("headache and migraine days") name migraine days without that condition and without a reference to OUT-005. OUT-009, OUT-021 and OUT-034 refer to OUT-005 by its ID.
- Effect on the model: by the reference rule of section 3.5, components that refer to OUT-005 by ID keep its condition (INV-035, INV-068, INV-104). Components named without the reference are modelled as stated, without the condition (INV-040, INV-056, INV-070, INV-105). For a subject without migraine (for example a preventive treatment for tension-type headache), these outputs show migraine days that are all 0.
- For the human: decide whether migraine-day components of OUT-018, OUT-022, OUT-028 and OUT-035 apply only to patients who have (or, for OUT-028, may have) migraine.

### ISS-04 The clinician-facing summary includes MAY measures at SHOULD level
- Stage 1: OUT-034 (SHOULD) brings together "frequency measures and their time course (OUT-004 to OUT-009)". The range includes OUT-008 (headache-free days, symptom-free days, periods without migraine days), which is MAY in its own requirement.
- Effect on the model: each part keeps its own strength (Stage 2 PROCESS.md section 4), so INV-104 includes headache-free days, symptom-free days and the marks of periods without migraine days in the clinician-facing summary at SHOULD. A diary that provides no OUT-008 measures at all, as OUT-008 permits, then deviates from the SHOULD of OUT-034.
- For the human: decide whether OUT-034 means OUT-008 measures "where provided".

### ISS-05 OUT-019 and the single count of the IHS position statement 2025
- Stage 1: OUT-019 asks for "the absolute number of migraine days and moderate/severe headache days per month that remain on treatment", citing [S-010]. OUT-020 names the "IHS position statement 2025 control levels" as a criterion.
- Evidence: [S-010] defines its levels on one count, the days with migraine or moderate-to-severe headache: "Modest Control. This is defined as four to six days with migraine or moderate-to-severe headache per month." (section "Setting goals of migraine burden while on treatment", p. 6).
- Effect on the model: OUT-019 is modelled as two counts (migraine days and moderate/severe headache days, E-044). The single count of [S-010] is modelled only as the value on which control-level labels rest (E-018, INV-062, INV-064), because OUT-020 requires the values a named criterion rests on.
- For the human: decide whether OUT-019's residual burden should also, or instead, show the single count of [S-010].

### ISS-06 "Total score" for instruments that have none
- Stage 1: OUT-026 asks for the "total score" of every validated instrument and names HURT and PGIC among them.
- Evidence: HURT grades its responses into areas rather than giving one total score: [S-014] "In either case, responses either fall into an area of “no concern” or are graded into one of three flagged areas indicating increasingly important treatment deficiencies; clinical advice is provided for each of latter." (quoted in Stage 1 OUT-026). PGIC is named by [S-008] among the "Patient Global Impression scales"; no source verified in Stage 2 defines a total score for it.
- Effect on the model: `totalScore` is SHOULD for every instrument as Stage 1 states it (E-058); categories are shown as published (`publishedCategory`). For HURT the SHOULD cannot be met, and the change from the baseline administration, which INV-082 relates to the total scores, then has no defined value.
- For the human: decide whether OUT-026 should read "total score, where the instrument defines one".

### ISS-08 Control levels under "responder or non-responder label"
- Stage 1: OUT-020 speaks of "a responder or non-responder label" and names the "IHS position statement 2025 control levels" as an example criterion. That criterion has four levels, not two.
- Evidence: [S-010] defines "Migraine Freedom", "Optimal Control", "Modest Control" and "Insufficient Control" (section "Setting goals of migraine burden while on treatment", p. 6; quoted in E-046).
- Effect on the model: the label category is either responder, non-responder or one of the four control levels (E-046); all other properties of OUT-020 apply to every category.
- For the human: confirm that control-level labels are responder labels in the sense of OUT-020.

### ISS-09 Which "acute medication outputs" OUT-029 breaks down by headache type
- Stage 1: OUT-029 (MUST) asks for "frequency and acute medication outputs separately for each headache type [...] as well as combined", without naming which acute-medication outputs it means. Group D of Stage 1 contains the acute-medication days of OUT-014 (total, by class and by drug), the weekly view of OUT-015 (SHOULD) and the medication-overuse indicator of OUT-016 (MUST).
- Evidence: the ICHD-3 8.2 levels to which the OUT-016 indicator refers concern the use of acute or symptomatic headache medication as such, not the medication taken for one headache type: [S-001] "[...] regular overuse of acute or symptomatic headache medication (on 10 or more or 15 or more days/month, depending on the medication) for more than three months." (8.2 Medication-overuse headache, Description, p. 122; quoted in E-032).
- Effect on the model: INV-028 presents the acute-medication days of OUT-014 (total, per class and per drug) for each headache type and combined. The weekly view (E-036, INV-025) and the medication-overuse indicator (E-032, INV-044) are required for all headache types combined only; an indicator per headache type would not correspond to the ICHD-3 levels.
- For the human: decide whether "acute medication outputs" in OUT-029 also covers the weekly view of OUT-015 and the medication-overuse indicator of OUT-016.

ISS-07 was withdrawn in iteration 01 (section 9).

No output was found in the Stage 2 research that EBM supports and Stage 1 lacks. No Stage 1 source was found to be outdated by a newer version during the Stage 2 research.

## 9. Withdrawn elements

No element (E-NNN) or invariant (INV-NNN) has been withdrawn (as of v02). One Stage 1 issue of section 8 has been withdrawn and is listed here so that its ID is not reused:

| ID | Name | Withdrawn in iteration | Reason |
|---|---|---|---|
| ISS-07 | Overlapping bands in two Stage 1 sources (a Stage 1 issue of section 8) | 01 | Not a gap or defect of Stage 1, which does not state the bands (review remark R01-12). The overlaps of the HALT-90 bands at 20 and of the IHS Q6 MIDAS baseline ranges at 20 remain described in the Notes of E-057 and E-045. |

## 10. Sources

New Stage 2 sources only; Stage 1 sources S-001 to S-046 are cited by their Stage 1 IDs. Access date for every URL below: 2026-10-21. For PubMed Central articles, the same full text can be read in machine-readable form at `https://www.ebi.ac.uk/europepmc/webservices/rest/<PMCID>/fullTextXML`, which is where the quotes were checked.

| ID | Citation | Type and grading | Language | Year | DOI / PMID | URL where quotes can be verified |
|---|---|---|---|---|---|---|
| S-101 | Yang M, Rendas-Baum R, Varon SF, Kosinski M. Validation of the Headache Impact Test (HIT-6™) across episodic and chronic migraine. Cephalalgia 2011;31(3):357–367. | Primary study (validation study), co-authored by M. Kosinski, a developer of HIT-6 (QualityMetric); no grading | English | 2011 | 10.1177/0333102410379890 / PMID 20819842 / PMC3057423 | https://pmc.ncbi.nlm.nih.gov/articles/PMC3057423/ |
| S-102 | Pavlovic JM, Stewart WF, Bruce CA, Gorman JA, Sun H, Buse DC, Lipton RB. Burden of migraine related to menses: results from the AMPP study. J Headache Pain 2015;16:24. | Primary study (population-based study), co-authored by W.F. Stewart and R.B. Lipton, the developers of MIDAS; no grading | English | 2015 | 10.1186/s10194-015-0503-y / PMID 25902814 / PMC4406925 | https://pmc.ncbi.nlm.nih.gov/articles/PMC4406925/ |
| S-103 | Cincinnati Children's Hospital Medical Center, Headache Center. "PedMIDAS Tool for Assessing Migraine Disability" (web page "PedMIDAS Tool"). PedMIDAS was developed at this centre (Hershey AD, Powers SW, Vockell AL, et al. PedMIDAS: development of a questionnaire to assess disability of migraines in children. Neurology 2001;57(11):2034–2039, PMID 11739822). | Instrument documentation by the developers' institution; no grading | English | current page (page footer © 2026) | — (developer paper: 10.1212/wnl.57.11.2034 / PMID 11739822) | https://www.cincinnatichildrens.org/service/h/headache-center/pedmidas |
| S-104 | Snaith RP. The Hospital Anxiety And Depression Scale. Health Qual Life Outcomes 2003;1:29. | Commentary by a co-developer of the instrument; no grading | English | 2003 | 10.1186/1477-7525-1-29 / PMID 12914662 / PMC183845 | https://pmc.ncbi.nlm.nih.gov/articles/PMC183845/ |
| S-105 | Instruction manual: Instructions for Patient Health Questionnaire (PHQ) and GAD-7 Measures. The PHQ family of measures and the GAD-7 "were developed by Drs. Robert L. Spitzer, Janet B.W. Williams, Kurt Kroenke and colleagues, with an educational grant from Pfizer Inc." (manual, P. 8/9, section "Questions regarding development, acknowledgments and use"). Undated; PDF created 2010, modified 2014 (document metadata, author Kurt Kroenke). Copy hosted by The Joint Commission. | Instrument documentation by the developers; no grading | English | 2010 (PDF metadata) | — | https://manual.jointcommission.org/pub/BHCInstruments/RomInstr00054/instructions_PHQ.pdf |

## 11. Search log

Search date: 2026-10-21. Tools: direct download with `curl` through the configured proxy; PubMed E-utilities (esearch, esummary, efetch); Europe PMC REST API (full-text XML); general web search; text extraction with `pdftotext` and Python `pypdf`. Every new quote in sections 5 and 8 was checked by script against the text downloaded from the URL listed in section 10 (or, for S-001, S-008, S-010 and S-014, in Stage 1 section 5), with whitespace, ligatures, line-end hyphens and glyphs without a text mapping (ICHD-3: "≥", "±", "−") normalised. One sentence of [S-010] is interrupted in the PDF text layer by a running header at a column break and was checked in its two parts.

| Language / region | Queries and sites | Found and used | Found but not used, not found, or unreachable |
|---|---|---|---|
| English — classification standard | ichd-3.org (ICHD-3 PDF, the Stage 1 URL of S-001); page-by-page search of the text layer for 8.2 and its subtypes, appendix A1.1, and "Definitions of terms". | [S-001] code labels (pp. 8, 9, 12), reference levels and time span of 8.2 and its subtypes (pp. 122–125), the perimenstrual window of A1.1.1 and A1.1.2 (p. 190), the duration of a cluster remission period (p. 209). | The "≥", "±" and "−" signs are glyphs without a text mapping in the PDF text layer; quotes give the signs as printed. "Simple analgesics" occurs only in section 10 (ISS-02). |
| English — IHS practice recommendations and position statement | ricerca.univaq.it PDFs of S-008 and S-010 (Stage 1 URLs). | [S-008] Q6: the chronic-migraine 30 % alternative and the MIDAS and HIT-6 thresholds (pp. 12–13). [S-010]: the four control levels (p. 6). | The AHS consensus statement that IHS Q6 cites for the MIDAS and HIT-6 thresholds (its reference 9) was not retrieved; the Stage 1 search log notes that Wiley returns HTTP 403 for AHS full texts. |
| English — MIDAS | PubMed: "Stewart WF[au] AND Lipton RB[au] AND MIDAS[ti]" (6 results); Europe PMC: "MIDAS AND AUTH:\"Stewart WF\" AND OPEN_ACCESS:y" (4 results); neurology.org (S-044 full text); web search "MIDAS questionnaire pdf Grade I Little or no disability Grade IV". | [S-102] (open access, MIDAS developers as co-authors): grade labels with score bands, recall period. | S-044 full text: neurology.org returned HTTP 403; Lipton et al. 2001 (Headache, PMID 11703471) and Stewart et al. 2000 (Pain, PMID 11098098): not open access. Other developer-co-authored open papers use other labels: PMC8684566 (2021, "little or none", "mild", "moderate", "severe") and PMC6537129 (2019, "minimal or infrequent disability", grades IVa and IVb); noted in E-057 Notes. headaches.org MIDAS form: HTTP 403 (also with a browser user agent); migrainecanada.org: HTTP 429; a hospital copy of the form (scripps.org) was downloaded but not used, being a third-party adaptation. |
| English — HIT-6 | PubMed: "Kosinski M[au] AND HIT-6[ti]" (3 results). | [S-101] (open access, co-authored by a HIT-6 developer): score range and the four impact categories with their bands. | Kosinski et al. 2003 (Qual Life Res, PMID 14651415): not open access. Rendas-Baum et al. 2014 (PMC4243819): found, not needed. The HIT-6 form itself is copyrighted and was not retrieved; the recall period follows Stage 1 ([S-002]). |
| English — PedMIDAS | PubMed: "Hershey AD[au] AND PedMIDAS[tiab] AND 2001[dp]" (1 result); web search "PedMIDAS questionnaire Cincinnati Children's grading". | [S-103] (developers' institution): the four disability grades with score ranges. | Hershey et al. 2001 (Neurology, PMID 11739822): not open access. NIH common-data-element form (nih.gov .docx): found, not used. No upper bound of the PedMIDAS score was found in a developer source; none is stated. |
| English — HALT and HURT | Europe PMC full texts of S-014 (Stage 1 source), PMC5796955 (HALT indices, 2018) and PMC5812954 (HURT, 2018). | [S-014]: HALT-90 and HALT-30 recall, units and the HALT-90 grading table. | The two 2018 developer papers print the same HALT-90 table and HURT description; not cited separately. HURT has no total score in these sources (ISS-06). |
| English — MSQ v2.1, M-TOQ, PGIC | PubMed: "\"Migraine-Specific Quality of Life\" AND (version 2.1 OR v2.1) AND (Martin BC[au] OR Jhingran P[au])" (1 result: Martin et al. 2000, Headache, PMID 10759923); "Lipton RB[au] AND Migraine Treatment Optimization Questionnaire[tiab]" (first 15 results reviewed). | — | MSQ v2.1 and M-TOQ developer papers are not open access (Wiley; SAGE returned HTTP 403 in Stage 1). PGIC exists in several versions with different wordings. Their value sets are therefore not tabulated; results show the instruments' own published scores and categories by name (E-057). |
| English — HADS, PHQ-9, GAD-7 | PubMed: "Snaith RP[au] AND Hospital Anxiety and Depression Scale[ti]"; "Kroenke K[au] AND Spitzer RL[au] AND PHQ-9[ti] AND 2001[dp]"; "Spitzer RL[au] AND GAD-7[ti] AND 2006[dp]"; pmc.ncbi.nlm.nih.gov; europepmc.org; phqscreeners.com; web search "phqscreeners.com instruction manual PHQ-9 GAD-7". | [S-104]: HADS subscale ranges. [S-105]: PHQ-9 and GAD-7 score ranges. | Kroenke et al. 2001 (PMC1495268): Europe PMC lists it as not open access and its PDF render returned HTTP 403; pmc.ncbi.nlm.nih.gov returned a browser-check page. Spitzer et al. 2006 (Arch Intern Med, PMID 16717171): not retrieved. phqscreeners.com: home page reached, no link to the manual found; the developers' manual was taken from the copy hosted by The Joint Commission. Zigmond and Snaith 1983 (PMID 6880820): not open access. |
| German | Web search "HIT-6 Auswertung Punktwert 36 bis 78 Kategorien \"schwere Beeinträchtigung\" Kopfschmerz Fragebogen". | — | No German-language source returned; results were English trial protocols that state the same HIT-6 range and categories as [S-101]. The DMKG/ÖKSG/SKG thresholds are those of S-023, quoted in Stage 1. |
| French, Italian | Web search "questionnaire MIDAS grade I II III IV score 0-5 6-10 11-20 21 handicap migraine interprétation". | — | French and Italian copies of the MIDAS form (for example aslroma1.it) use the same score bands with translated labels; not used, because the model states the labels of the developer-co-authored English source. |
| Spanish | Web search "PedMIDAS grados discapacidad 0-10 11-30 31-50 >50 cuestionario migraña infantil validación española". | — | No Spanish PedMIDAS validation with grade labels found; a Spanish MIDAS validation (PMC7038557) was found and not needed. |
| Other languages | — | — | The value sets added in Stage 2 are defined by English-language standard owners and instrument developers; national-language versions are translations with the same score bands. Stage 1's multilingual sources (for example S-023, German; S-033, Russian) are reused by their Stage 1 quotes for responder criteria (E-045). No further languages were searched in this iteration. |

Iteration 01 (fix, 2026-10-21): no new searches. To verify review remarks, the following were downloaded again with `curl` into a fresh directory outside the repository and checked by script: the Stage 1 URLs of [S-028] (NVN module page, HTTP 200; the Aanbeveling contains the OUT-018 quote and begins with the advice to start prophylactics low and titrate slowly), [S-033] (official PDF, 92 pages; the OUT-018 quote is in section 7.1 "Оценка эффекта проводимой терапии", p. 53) and [S-001] (8.2 Description, p. 122); the Europe PMC full texts of [S-014], [S-101] and [S-102]; the [S-103] page; and the [S-105] PDF (the developers sentence is on page "P.8/9"). No new source was added.

Iteration 02 (fix, 2026-10-21): no new searches and no new source; the iteration 02 remarks concern the formal model. To verify them, the Stage 1 URL of [S-015] (NICE CG150 recommendations page, HTTP 200) was downloaded again with `curl` into a fresh directory outside the repository: recommendation 1.3.29 reads "after 2 treatment cycles", the time point that `ruleNice1329` anchors at the end of the second cycle with no further offset. The [S-001] PDF (211 pages) was downloaded again and page 190 extracted: the A1.1.1 window and note 2 used by INV-087 are as quoted in E-060.

## 12. Change log

- v00 (iteration 00, 2026-10-21): Initial draft by the author. Notation OMN defined (section 2). 67 elements (E-001 to E-067) and 105 invariants (INV-001 to INV-105) realising all 39 Stage 1 requirements, each traced with full coverage (section 7). Thresholds, reference levels, offsets and score bands that are part of the output data are stated with verbatim quotes: ICHD-3 codes, the 8.2 reference levels and time span, the A1.1 perimenstrual window and the remission duration ([S-001]); the IHS Q6 thresholds ([S-008]) and IHS 2025 control levels ([S-010]); HALT recall, units and grading ([S-014]); HIT-6, MIDAS, PedMIDAS, HADS, PHQ-9 and GAD-7 value sets (new sources S-101 to S-105). Eight Stage 1 issues listed (ISS-01 to ISS-08). Mechanical checks run by script (IDs, references, declared names, attribute selections, traceability, conformance levels against Stage 1 statement strength).
- v01 (iteration 01, 2026-10-21): Fix of review iteration 01 (12 remarks; fixes/fix-iter-01.md).
  - R01-01: evaluation rules `ruleNvnTitrated` (NVN, 2–3 months, titrated prophylactics) and `ruleRu71` (Russian section 7.1, 3 months) added to E-041; E-041 Notes and the OUT-018 row now describe the rule list accurately.
  - R01-02: INV-001 requires a guidance type for every preventive treatment (`otherPreventive` as fallback); E-008 and E-041 Notes.
  - R01-03: baseline and on-treatment periods of a response comparison are calendar months or 28-day periods, and every change of a comparison compares its on-treatment and baseline values (INV-056, E-043); INV-061 refers to the compared period itself when that is monthly (E-044 Notes).
  - R01-04: the reduction relations of E-046 decide only labels with a single evaluated period (`reductionMet`, `reductionDecided`, INV-063 Reading, E-046 Notes).
  - R01-05: claim `continuationDecision` (E-001) and INV-106 (MUST NOT); the same kind of gap for the OUT-023 Caveat fixed by claim `acuteResponseDefinitionDecision` and INV-107 (SHOULD NOT); new section 6.12.
  - R01-06: INV-028 requires the per-class and per-drug acute-medication days per headache type; the model's reading of "acute medication outputs" stated as ISS-09 (new), with pointers from E-029, E-032, E-036 and INV-028.
  - R01-07: INV-072 requires every summarised treated attack to be listed with a result for every outcome measure; E-051 `sequence` SHOULD only when there are treated attacks.
  - R01-08: `CycleLine.complete` added; INV-087 defines `completeCycles` over the cycles shown, lets only the last cycle be unfinished, fixes its span and requires the cycles to be items of the view.
  - R01-09: INV-104 requires the time course of migraine days, moderate/severe headache days and attacks, the marks of periods without migraine days and the days with severe functional impairment; ISS-04 updated; the Conformance of E-020 to E-022 points to INV-104.
  - R01-10: `high = ∅` now means "the model states no upper bound"; `wholeNumberScores` (MIDAS, HIT-6, PedMIDAS, HALT-90, HALT-30) and the whole-number conjunct of INV-082; ℕ₁ ⊆ ℕ ⊆ ℤ ⊆ ℚ stated in section 2.8.
  - R01-11: S-105 location corrected to P. 8/9.
  - R01-12: ISS-07 withdrawn (section 9); E-046 Notes point to ISS-08; E-028 Notes point to ISS-01.
  - Totals: 67 elements (E-001 to E-067) and 107 invariants (INV-001 to INV-107); eight Stage 1 issues (ISS-01 to ISS-06, ISS-08, ISS-09; ISS-07 withdrawn).
- v02 (iteration 02, 2026-10-21): Fix of review iteration 02 (7 remarks; fixes/fix-iter-02.md), with a satisfiability pass over all MUST and SHOULD constraints.
  - R02-01: INV-055 requires the comparison at a time point only where a calendar month or 28-day period beginning on or after the treatment start can end at it (new `shortestMonthlyDays` and `fitsMonthlyPeriod`, E-042); INV-001 states that no course event of a treatment precedes its start; E-041, E-043 Notes; OUT-018 row.
  - R02-02: (a) INV-104 requires the time-course series only when the covered period contains a whole period (new `containsPeriodOf`, E-006); the mark of the covered period without migraine days is required outside that condition. (b) INV-039 requires, for children and adolescents, comparisons of selections of equal length only (OUT-036 (c)); E-037 Conformance; OUT-010 and OUT-034 rows.
  - R02-03: INV-068 requires the per-class and per-drug acute-medication days for every baseline and on-treatment period; E-048 Meaning and Conformance; OUT-021 row.
  - R02-04: INV-027 requires the days with severe functional impairment for the baseline and on-treatment periods; E-030 Conformance; OUT-027 row.
  - R02-05: the duration of a treatment that has not stopped runs to the as-of date (E-055, INV-079); `duration` and `startDate` SHOULD only when the treatment has a start; OUT-024 row.
  - R02-06: INV-076 applies to every treated-attack line of a subject with migraine, as INV-022 and E-053 do; OUT-012 row.
  - R02-07: INV-105 requires a cycle line that overlaps the covered period; OUT-035 row.
  - Other changes from the sweep: INV-087 states the relations of cycle lines and attack marks for every view that shows them (Realises +OUT-035); E-055 `preventiveResponse` and `adherence` SHOULD only for a treatment that has a start; E-049 `onTreatmentPeriod` SHOULD only when the event falls after the start day; E-058 `baselineResult` SHOULD only when an earlier result is available; INV-062 and E-046 `otherValues` require the other values of a criterion only where they are available (new `valueAvailable`, E-045); E-062 `acute` SHOULD only for a subject who uses acute medication; INV-105 requires treatment effect only for a started preventive treatment or used acute medication; INV-075 shows each symptom status once (Realises +OUT-012); ISS-06 notes the consequence for the change from baseline; INV-001 Realises +OUT-024; INV-076 heading.
  - Totals: 67 elements (E-001 to E-067) and 107 invariants (INV-001 to INV-107), no element or invariant withdrawn; levels unchanged (MUST 18, MUST NOT 2, SHOULD 47, SHOULD NOT 8, definitional 32); no new source.
