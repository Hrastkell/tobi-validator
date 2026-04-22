# Tsubasa Stage 1 Public Syntax and Authoring Reference

**Status:** Public-safe Stage 1 reference  
**Scope:** Current public Stage 1 Tsubasa authoring corridor for external teams, third-party AI agents, evaluators, and GitHub/CI users  
**Product line:** AI Verification Engine / Tobi Validator  
**Boundary note:** This document is the most complete public Stage 1 syntax-and-authoring reference currently possible from the project-safe corpus. It does **not** claim full long-term language completeness. Semantic authority remains outside this document. Shipped truth remains validator-first, narrow, and aligned with the current Stage 1 released contour.

---

## 1. Purpose

This document exists to solve a practical public-documentation gap.

The public corpus already contains:
- narrow quickstarts,
- agent discipline notes,
- golden-style examples,
- language/compiler status,
- product positioning documents.

What it has lacked is one dense public reference that explains, as fully and honestly as current public-safe evidence allows:

- what external teams may safely write today,
- what current validator-facing syntax patterns are visible,
- what should be treated as surface authoring,
- what should be treated as canonical truth,
- how canonicalization and convergence work in practice,
- how to write Stage 1 artifacts without inventing unsupported semantics.

This document is for:
- external engineering teams,
- third-party AI agents,
- GitHub/CI users,
- evaluators,
- users who need validator-meaningful Tsubasa artifacts under the current shipped Stage 1 corridor.

It is **not**:
- a new semantic authority,
- a spec-core replacement,
- a claim of full long-term grammar completeness,
- a statement of runtime or backend maturity.

---

## 2. First Safe Mental Model

In current public Stage 1, Tsubasa should **not** be read as:
- a general scripting language,
- a backend language,
- a runtime language,
- a broad platform language,
- a public proof that every future language feature is already known.

The current public-safe mental model is narrower and more operational:

> Tsubasa is the semantic layer for canonical reasoning artifacts.  
> Tobi is the reference validator that accepts, rejects, canonicalizes, and compares those artifacts.

That means good Stage 1 authoring is:
- small,
- explicit,
- validator-meaningful,
- canonicalization-aware,
- reviewable,
- narrow enough to preserve pass/fail clarity.

A practical loop is:

```text
produce
→ validate
→ inspect canonical output
→ compare
→ refine
```

The core discipline is simple:

> trust validator output more than prose intuition, and trust canonical output more than raw surface appearance.

---

## 3. Current Public Stage 1 Scope

### What this document does cover

This document covers:
- the current validator-first model,
- the current public Stage 1 authoring corridor,
- the locked canonical pipeline doctrine,
- current visible authoring forms,
- current sequencing truth,
- current decimal convergence guidance,
- accepted and rejected example families,
- practical interpretation of canonical output and `_h`,
- practical workflow for external AI agents.

### What this document does not cover

This document does **not** cover:
- a full long-term formal grammar of all future Tsubasa,
- backend or runtime semantics,
- code generation,
- a shipped verification API,
- unrestricted language breadth,
- a full platform language,
- future syntax that is not public-safe today.

### Reading rule

Where the public-safe corpus is strong, this document speaks directly.

Where the public-safe corpus is narrower, this document uses disciplined phrases such as:
- **current public Stage 1 truth**
- **current validator-facing reading**
- **public-safe guidance**
- **observed Stage 1 authoring pattern**
- **must not be read as broader long-term completeness**

That distinction is intentional and necessary.

---

## 4. Current Public Stage 1 Product Context

The current released first product remains:

**AI Verification Engine / Tobi Validator**

Its truthful shipped Stage 1 contour is intentionally narrow. Public-safe current truth includes:
- installable validator CLI,
- canonical ASCII output,
- `_h` hash output,
- deterministic diagnostics,
- conformance / golden execution,
- thin packaging,
- install / usage framing.

Public-safe current truth does **not** include:
- shipped backend maturity,
- shipped runtime maturity,
- shipped verification API,
- broad platform surface,
- unrestricted execution environment claims.

This matters because external authors must not infer language breadth from internal compiler or trunk depth.

---

## 5. Lexical / Surface Authoring Layer

This section describes the surface authoring layer only to the extent that current public-safe evidence supports it.

### 5.1 Identifiers

Current public-safe examples visibly support identifier-shaped names such as:

```tsubasa
x
y
pid
```

Canonical output also visibly uses forms such as:

```text
ID(x)
ID(y)
```

Public-safe guidance:
- simple alphabetic identifiers are clearly part of current authoring reality,
- short, explicit names are safest,
- do not infer full namespace, module, or package systems from current public examples.

### 5.2 Visible keywords and authoring words

Current public-safe examples visibly support authoring words such as:
- `let`
- `in`
- `atomic`

Examples:

```tsubasa
let x = 1 in x
```

```tsubasa
atomic{ let x = 1 in x; let y = 2 in y }
```

Public-safe guidance:
- prefer forms already visible in current validator-facing examples,
- do not extrapolate broader keyword families unless you have validator-confirmed evidence.

### 5.3 Delimiters and punctuation

Current public-safe surface evidence visibly includes:
- braces `{ }`,
- parentheses `( )`,
- commas `,`,
- equals sign `=`,
- semicolon `;`,
- sequencing skin `▷`.

Important distinction:
- some punctuation belongs to **surface authoring**,
- some belongs to **canonical output**,
- they are not equal in authority.

For example:
- `;` and `▷` may be authored as sequencing skins,
- they are **not** canonical sequencing truth,
- canonical sequencing output remains `seq([...])`.

### 5.4 Whitespace

Current public-safe guidance:
- use normal explicit spacing,
- avoid compressed symbol-heavy writing,
- do not assume whitespace-sensitive semantics unless validator behavior proves it for your exact case.

### 5.5 Unicode and normalization caution

The locked canonical doctrine includes normalization and alias/canonical mapping.

That means current public-safe authoring should assume:
- normalization happens,
- alias/canonical mapping happens,
- visually different surface can converge to the same canonical result,
- confusable symbols should be treated with caution.

### 5.6 Confusable character caution

Public-safe guidance:
- do not invent symbol-heavy syntax,
- do not assume visually similar characters are distinct semantic constructs,
- prefer plain reviewable source,
- treat canonical output as the actual public truth surface.

### 5.7 Decimal and malformed literal caution

Current public-safe evidence supports:
- decimal convergence,
- malformed numeric rejects.

Safe assumption:
- multiple equivalent decimal surface forms may converge,
- malformed numeric forms may reject early,
- authors should prefer clear decimal writing and validate.

Unsafe assumption:
- that every visually plausible numeric form is accepted,
- that decimal formatting differences will remain visible after canonicalization.

---

## 6. Core Authoring Forms Currently Visible in Stage 1

This section gathers the most complete list of forms that can be publicly and honestly described today.

It does **not** claim total long-term completeness. It describes what is visibly current, validator-meaningful, and public-safe.

### 6.1 Binding form

**Name:** binding / let-form  
**Purpose:** introduce a local value and continue inside a narrow expression context  
**Authoring shape:**

```tsubasa
let x = 1 in x
```

**Accepted example:**

```tsubasa
let x = 1 in x
```

**Public-safe canonical reading:**

```text
bind(ID(x), DEC(1), ID(x))
```

**Caution:**
- do not invent alternative binder keywords,
- do not infer a broad declaration system from this alone,
- do not treat source variable naming as semantic authority.

### 6.2 Identifier reference

**Name:** identifier reference  
**Purpose:** refer to a previously introduced local identifier  
**Authoring shape:**

```tsubasa
x
```

**Accepted example:**

```tsubasa
let x = 1 in x
```

**Public-safe canonical reading:**

```text
ID(x)
```

**Caution:**
- current public evidence supports simple local identifier use,
- it does not by itself prove a broad public namespace system.

### 6.3 Decimal literal

**Name:** decimal literal  
**Purpose:** provide a numeric value under the current Stage 1 numeric discipline  
**Authoring shapes visibly supported today:**

```tsubasa
1
1.0
01.000
```

**Accepted example family:**

```tsubasa
let x = 1 in x
let x = 1.0 in x
let x = 01.000 in x
```

**Public-safe canonical reading:**

Equivalent surface decimal forms may converge to:

```text
DEC(1)
```

**Caution:**
- this is convergence, not semantic widening,
- malformed numeric forms may reject,
- do not assume every plausible numeric formatting style is part of current truth.

### 6.4 Atomic block

**Name:** atomic block  
**Purpose:** mark a narrow block-shaped authoring context visible in the current Stage 1 corridor  
**Authoring shape:**

```tsubasa
atomic{ let x = 1 in x; let y = 2 in y }
```

**Accepted example:**

```tsubasa
atomic{ let x = 1 in x; let y = 2 in y }
```

**Public-safe reading:**
- `atomic{ ... }` is visibly part of the current validator-facing corridor,
- it should be read conservatively,
- it must not be overinterpreted as proof of broader runtime or concurrency maturity.

**Caution:**
- do not infer full execution semantics from the public-safe Stage 1 presence of `atomic`.

### 6.5 Sequencing skins

**Name:** sequencing skins  
**Purpose:** allow surface sequencing in authoring  
**Authoring shapes:**

```tsubasa
a ; b
a ▷ b
```

**Accepted example family:**

```tsubasa
atomic{ let x = 1 in x; let y = 2 in y }
atomic{ let x = 1 in x ▷ let y = 2 in y }
```

**Canonical truth:**

```text
seq([...])
```

**Caution:**
- `;` and `▷` are not separate canonical operators in public Stage 1 reading,
- they are skins only,
- they must not be read as canonical output truth.

---

## 7. Canonicalization and Convergence

This is one of the most important sections in the document.

### 7.1 Locked canonical doctrine

Current locked canonical doctrine is:

```text
parse
→ NFC normalize
→ alias → canonical
→ desugar
→ canonical Core AST
→ canonical ASCII
→ TSER
→ _h
```

### 7.2 Public-safe operational reading

For external users, the most practical current reading is:

- source is parsed,
- normalization happens,
- alias/canonical mapping happens,
- desugar may happen,
- canonical meaning is stabilized,
- canonical ASCII is produced,
- `_h` is produced as compatibility identity.

Important current tooling note:
- the doctrine includes `TSER`,
- but current public Stage 1 tooling should **not** be assumed to expose TSER as a separately inspectable first-class surface.

### 7.3 What each step means, operationally

**parse**  
The source is accepted or rejected as current validator-facing syntax.

**NFC normalize**  
Unicode normalization removes avoidable instability.

**alias → canonical**  
Input skins and variants may converge before final canonicalization.

**desugar**  
Surface-level conveniences may lower into existing core structures.

**canonical Core AST**  
Meaning stabilizes in canonical internal structure.

**canonical ASCII**  
The most important current inspectable canonical surface for external users.

**TSER**  
Part of locked doctrine, but not something external Stage 1 users should assume they can always inspect separately in tooling.

**`_h`**  
Compatibility identity derived through the locked pipeline.

### 7.4 Why convergence matters

The point of the pipeline is reproducibility, not mystique.

It means:
- stylistic source differences should not be mistaken for semantic differences,
- the validator decides accepted canonical reading,
- compare by canonical result, not by raw source appearance.

### 7.5 Surface truth vs canonical truth

This is a central Stage 1 discipline rule:

> surface text is what you write; canonical output is what the validator trusts.

That distinction is essential for human users and AI agents alike.

---

## 8. Sequencing Truth

This area must remain especially explicit.

### 8.1 What may be authored

Current public-safe authoring may include sequencing skins such as:

```tsubasa
;
▷
```

### 8.2 What is canonical

Current canonical sequencing truth is:

```text
seq([...])
```

### 8.3 What this means in practice

You may write:

```tsubasa
atomic{ let x = 1 in x; let y = 2 in y }
```

or:

```tsubasa
atomic{ let x = 1 in x ▷ let y = 2 in y }
```

But you must **not** treat `;` or `▷` as canonical output truth.

### 8.4 What must not be assumed

Do **not** assume:
- that `;` and `▷` are separate long-term canonical operators,
- that current sequencing skins imply broader future sequencing doctrine,
- that surface punctuation is semantically stronger than canonical output.

### 8.5 Safe engineering rule

Author with accepted skins if needed, but compare and reason through `seq([...])`, not through surface punctuation.

---

## 9. Numeric / Literal Discipline

### 9.1 Decimal convergence

Current public-safe Stage 1 behavior supports decimal convergence across equivalent surface forms.

Observed family:

```tsubasa
let x = 1 in x
let x = 1.0 in x
let x = 01.000 in x
```

Public-safe current reading:
- these may converge to the same canonical decimal result,
- they are useful for conformance-style thinking,
- they are good current examples for external teams.

### 9.2 What agents should assume

Safe assumption:
- decimal surface writing may converge under canonicalization,
- compare canonical result rather than raw source.

Unsafe assumption:
- that every visually plausible numeric form is part of accepted current syntax,
- that malformed decimal forms will normalize instead of rejecting,
- that the full long-term numeric policy is fully public.

### 9.3 Malformed numeric caution

Malformed numeric forms can reject.
A reject-oriented example such as:

```tsubasa
let x = 01..0 in x
```

should be read as a malformed current-syntax example, not as a runtime-related case.

### 9.4 Exactness and conservatism

The current public-safe numeric reading is conservative:
- prefer small explicit decimals,
- validate rather than assume,
- treat convergence as validator behavior, not permission to become sloppy.

---

## 10. What Accepted Authoring Should Look Like

Current accepted Stage 1 authoring should look:
- small,
- explicit,
- narrow,
- reviewable,
- validator-meaningful,
- pass/fail meaningful,
- reusable in conformance-style testing.

Good Stage 1 authoring typically has:
- short artifacts,
- clear binding structure,
- minimal skin ambiguity,
- no runtime storytelling,
- no unsupported semantic claims,
- no pretend platform wrappers,
- no policy prose masquerading as syntax.

A useful rule is:

> if the artifact cannot be easily reviewed, canonicalized, and compared, it is probably too broad for the current public Stage 1 corridor.

---

## 11. What Agents Must Not Invent

This blacklist is strict.

External AI agents and external teams must **not** invent:
- runtime syntax,
- backend syntax,
- API surface claims,
- generic parser-DSL claims,
- regex engine claims,
- metadata wrapper layers,
- broad policy prose pretending to be syntax,
- broad future constructs,
- broad platform wrappers,
- runtime-starting constructs,
- verification API constructs,
- unsupported module systems,
- unsupported package systems,
- unsupported macro systems.

They must also not assume that internal trunk/compiler depth equals public authoring truth.

### Liu-specific caution

Liu remains sugar only.

Therefore agents must not treat Liu convenience as:
- new semantics,
- local doctrine,
- a second authority layer,
- a bypass around canonicalization.

If a Liu-authored artifact fails to preserve canonical truth after desugar, that is a Liu defect, not a semantic widening of Tsubasa.

---

## 12. Accepted Example Families

This section is intentionally example-rich.

Examples are not semantic authority, but they are practical guidance.

### 12.1 Accepted simple cases

#### Example 1 — minimal binding

```tsubasa
let x = 1 in x
```

Use:
- narrow valid artifact,
- baseline authoring shape,
- simple validator round-trip.

#### Example 2 — another minimal binding

```tsubasa
let y = 2 in y
```

Use:
- same family,
- good for minimal regression checks.

#### Example 3 — short atomic form

```tsubasa
atomic{ let x = 1 in x; let y = 2 in y }
```

Use:
- simple sequencing family,
- block-shaped authoring,
- canonical sequencing comparison.

### 12.2 Accepted variant family

#### Decimal convergence family

```tsubasa
let x = 1 in x
let x = 1.0 in x
let x = 01.000 in x
```

Current public-safe interpretation:
- same-meaning convergence family,
- useful for canonical comparison,
- useful for CI regression.

#### Sequencing convergence family

```tsubasa
atomic{ let x = 1 in x; let y = 2 in y }
atomic{ let x = 1 in x ▷ let y = 2 in y }
```

Current public-safe interpretation:
- same sequencing family,
- same canonical sequencing truth,
- good for skin-versus-canonical training.

### 12.3 Same-meaning / same-canonical-form families

These are some of the best families for external AI agents to learn from.

Preferred pattern:
- surface differs,
- canonical result converges,
- `_h` is expected to converge,
- validator demonstrates sameness better than prose.

### 12.4 Rejected malformed siblings

#### Reject sibling 1 — invented syntax

```tsubasa
let! x := 1 => x
```

Why useful:
- looks plausible,
- not part of current accepted corridor,
- strong anti-hallucination example.

#### Reject sibling 2 — malformed decimal

```tsubasa
let x = 01..0 in x
```

Why useful:
- malformed current-syntax example,
- useful as a concrete reject-oriented sibling,
- must not be interpreted as runtime-related.

### 12.5 Rejected confusable siblings

Confusable siblings are source forms that look almost valid but cross a boundary through:
- invented punctuation,
- unsupported skin assumptions,
- future-looking syntax,
- prose-instead-of-syntax.

Use them to teach agents not to hallucinate probable language forms.

### 12.6 Golden-oriented family shapes

Good Stage 1 golden-oriented family shapes include:
- minimal binding family,
- decimal convergence family,
- sequencing skin convergence family,
- malformed sibling reject family,
- confusable sibling family.

These are safer and more productive than broad speculative examples.

---

## 13. Pattern Catalog for External Teams

This section is organized by operational pattern.

### 13.1 Boundary family

Purpose:
- stay inside current shipped truth,
- avoid trunk/platform overreach,
- keep artifacts narrow.

Typical shape:
- one or two bindings,
- short sequencing chain,
- no runtime implications.

### 13.2 Convergence family

Purpose:
- prove that stylistic variants converge to one canonical result.

Typical use:
- same-meaning decimal variants,
- sequencing skins converging to `seq([...])`.

### 13.3 Minimal CI gate family

Purpose:
- small artifacts suitable for pass/fail checks in CI.

Traits:
- deterministic,
- reviewable,
- short,
- easy to inspect in canonical ASCII.

### 13.4 Reviewable regression family

Purpose:
- easy to store,
- easy to compare,
- easy to rerun after validator changes.

Traits:
- explicit,
- narrow,
- canonicalization-focused.

### 13.5 Malformed sibling family

Purpose:
- teach what current corridor rejects,
- prevent hallucinated expansion,
- improve agent discipline.

Traits:
- looks almost valid,
- rejected for real syntax/canonical reasons,
- useful as safety examples.

---

## 14. Output Interpretation

External teams should read validator output functionally.

### 14.1 What `CANON` means

`CANON` refers to the canonical form produced by the validator.

In current public Stage 1, canonical ASCII is the most important inspectable canonical surface.

Use it to answer:
- what meaning the validator accepted,
- whether surface variants converged,
- whether your expectation matched the actual accepted structure.

### 14.2 What `_h` means

`_h` is the compatibility identity produced through the locked canonical doctrine.

Practical Stage 1 reading:
- if canonical meaning converges, compatibility identity should converge,
- compare through canonical result, not raw source text alone.

### 14.3 What `reject` means

A reject means the validator did not accept the artifact under the current corridor.

Current public-safe reading:
- reject is useful signal,
- reject is part of the product,
- reject often means the artifact stepped outside the current validator-facing corridor.

### 14.4 How to read diagnostics

Current Stage 1 diagnostics should be read conservatively:
- they explain validator truth,
- they do not create new semantics,
- they help locate what failed,
- they should not be overread as total long-term grammar doctrine.

Where current corpus aligns, Stage 1 semantic diagnostics include the current Static Semantics MVP family, including E100–E107.

---

## 15. Practical Workflow for External AI Agents

### 15.1 Learn from accepted narrow examples

Start with:
- minimal bindings,
- decimal convergence families,
- sequencing convergence families.

Do not begin by attempting broad syntax exploration.

### 15.2 Narrow artifacts aggressively

When uncertain:
- make the artifact smaller,
- remove speculative syntax,
- reduce moving parts,
- validate again.

### 15.3 Use canonical output as feedback

The best current learning loop is:

1. write a narrow artifact,  
2. validate,  
3. inspect canonical ASCII,  
4. compare with expectation,  
5. refine.

### 15.4 Use golden-style families

Instead of inventing new syntax families, create small test families:
- valid baseline,
- accepted variant,
- same-meaning convergence sibling,
- malformed reject sibling.

This is far safer than free-form expansion.

### 15.5 Do not overreach

If public syntax completeness is not total, do not fill the gap with fantasy.

Correct behavior is:
- stay narrow,
- validate,
- observe,
- learn from canonical output,
- stop before unsupported semantics are invented.

---

## 16. Public-Safe Non-Goals

This document is **not**:
- a full runtime language guide,
- a platform language guide,
- a backend language reference,
- a verification API reference,
- a full long-term formal grammar of all Tsubasa,
- a claim of shipped platform maturity,
- a claim of broad product execution maturity,
- a claim that trunk/compiler depth equals public syntax authority.

It must not be used to imply:
- runtime/backend maturity,
- broad API maturity,
- platform SDK maturity,
- unrestricted language breadth,
- future roadmap semantics as present truth.

---

## 17. Glossary

**artifact**  
A Tsubasa input intended for validator acceptance, canonicalization, comparison, and compatibility identity.

**canonical ASCII**  
The canonical text output produced by the validator after canonicalization. In current public Stage 1, this is the primary inspectable canonical surface.

**convergence**  
The situation in which different surface forms lead to the same canonical result and compatibility identity.

**validator-facing**  
Written to match current real validator behavior rather than future language ambition.

**`_h`**  
Compatibility identity derived through the locked canonical doctrine.

**reject sibling**  
A nearby example that looks plausibly similar to a valid case but is expected to reject.

**surface skin**  
A surface authoring form that is allowed for input but is not canonical truth.

**canonical truth**  
What the validator preserves after normalization, alias mapping, desugar, and canonicalization.

**golden**  
A stable example or fixture family used for conformance and regression checking.

**conformance**  
Agreement with the validator-defined current operational corridor.

---

## 18. Source Basis

Source basis:
- 01_ORGANETIC_SYSTEM_STATUS.txt
- 02_ORGANETIC_PROJECT_CONTROL_MAP.txt
- 04_ORGANETIC_ROADMAP.txt
- 05_ORGANETIC_LANGUAGE_AND_COMPILER_STATUS.txt
- 06_LIU_DESUGAR_AND_INTEROP_SPEC.txt
- 07_PRODUCT_AND_STRATEGY_ARCHITECTURE.txt
- current public Stage 1 doc pack
- historical input only where useful: earlier quickstart/reference material, treated as rewrite source rather than authority

---

## 19. Bottom Line

An external team can safely do the following today:
- write narrow validator-meaningful Tsubasa artifacts,
- use simple binding forms,
- use small sequencing examples,
- use decimal convergence examples,
- validate through Tobi,
- compare through canonical ASCII and `_h`,
- build CI gates around current narrow accepted behavior.

An external team must **not** assume:
- full runtime language breadth,
- backend maturity,
- verification API maturity,
- unrestricted syntax completeness,
- broad platform truth.

The productive way to start is simple:

1. begin with narrow accepted examples,  
2. validate everything through Tobi,  
3. learn from canonical output,  
4. treat `seq([...])` as canonical sequencing truth,  
5. treat `;` and `▷` as skins only,  
6. keep artifacts small, explicit, and reviewable,  
7. stay inside the validator-first Stage 1 corridor.

That is the safest and most useful public Stage 1 reading of Tsubasa currently available.
