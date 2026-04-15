# Stage 1 Diagnostics Reference

Project: Organetic Sphere  
Component: Tobi  
Product: AI Verification Engine / Tobi Validator  
Scope: operator reference for current shipped validator diagnostics  
Date basis: 2026-04-15

## What This Doc Is For

This document is a practical operator reference for the current shipped validator diagnostics.

Use it to answer:

- what an error code usually means
- whether the failure is earlier-source rejection or semantic rejection
- what to check first before reporting an issue
- how to distinguish source-validation failure from `golden` mismatch

This document is not:

- semantic authority
- a promise of broader platform behavior
- a runtime/backend/API guide

For issue classification and the exact Stage 1 reproduction checklist, use:

- `docs/STAGE1_SUPPORT_AND_ISSUE_REPORTING.md`

## Reading Model

There are three main outcomes in the shipped validator workflow:

### Accepted Input

If input is accepted by the current validator, `canon` produces:

- `CANON:`
- canonical ASCII
- `HASH:`
- current `_h` rendered as hex

### Rejected Input With Diagnostics

If input is rejected, the validator returns a diagnostic code, message, and usually a span.

Practical rule:

- earlier ingress / lexer / parser rejection means the input was not accepted at all
- `E100`-`E107` means the input parsed far enough to hit current shipped static-semantics checks

### Conformance / Golden Mismatch

`golden` mismatch is different from source rejection.

It means:

- the fixture expected one result
- the current validator produced another result

Typical `golden` mismatch classes in the shipped runner include:

- canonical mismatch
- hash mismatch
- error code mismatch
- error message-class mismatch
- error span mismatch

This is a conformance expectation failure, not automatically a parser or semantic acceptance failure.

## Error-Code Reference

This reference covers the shipped semantic diagnostic range:

- `E100`
- `E101`
- `E102`
- `E103`
- `E104`
- `E105`
- `E106`
- `E107`

### `E100` - semantic call arity mismatch

- Short meaning:
  - a builtin was called with the wrong number of arguments
- Typical cause:
  - calling `to_dec`, `to_flt`, `__not`, `__and`, `__or`, or comparison/equality forms with too few or too many arguments
- What to check first:
  - the callee name
  - the expected argument count for that builtin
  - whether an optional context argument is the only extra argument in `to_dec` / `to_flt`
- Usual class:
  - callable/use-shape issue

### `E101` - semantic exact-decimal type mismatch

- Short meaning:
  - a strict exact-decimal comparison received the wrong type
- Typical cause:
  - `__lt`, `__le`, `__gt`, or `__ge` received a non-`Dec` value where exact decimal comparison is required
- What to check first:
  - whether both comparison inputs are exact decimals
  - whether you accidentally passed `Bool`, `String`, or another incompatible value
  - whether you expected float-like comparison instead of exact decimal comparison
- Usual class:
  - typing issue

### `E102` - semantic builtin argument type mismatch

- Short meaning:
  - the call shape is valid, but one or more builtin arguments have the wrong type
- Typical cause:
  - boolean builtin received non-boolean input
  - equality operands have incompatible types
  - `to_dec` / `to_flt` optional context argument is not a string
- What to check first:
  - the builtin being called
  - the type of each argument at the exact reported span
  - whether mixed-type equality or wrong context-argument type was used
- Usual class:
  - typing issue

### `E103` - semantic match arm result type mismatch

- Short meaning:
  - match arms do not return the same result type
- Typical cause:
  - one arm returns a decimal-like result while another returns string/bool/other type
- What to check first:
  - each arm result expression
  - whether one arm accidentally returns a different type than the others
- Usual class:
  - typing issue

### `E104` - semantic atomic/effect boundary violation

- Short meaning:
  - an atomic-only or effectful expression was used in the wrong context
- Typical cause:
  - `to_flt(...)` used outside `atomic{...}`
  - effectful expression such as `atomic{...}` or `note ...` used where a pure value is required
- What to check first:
  - whether the operation must be inside `atomic{...}`
  - whether an effectful expression appears in a pure value position
  - the exact span, because it usually points directly at the boundary violation source
- Usual class:
  - atomic/barrier issue

### `E105` - semantic explicit barrier required

- Short meaning:
  - exact decimal comparison requires an explicit barrier conversion
- Typical cause:
  - floatish value from `to_flt(...)` was compared without an explicit `to_dec(...)` barrier
- What to check first:
  - whether comparison input came from `to_flt(...)`
  - whether an explicit `to_dec(...)` conversion is missing before exact decimal comparison
- Usual class:
  - atomic/barrier issue

### `E106` - semantic pattern type mismatch

- Short meaning:
  - the pattern does not match the scrutinee type expected by the current validator
- Typical cause:
  - boolean pattern used against a non-boolean scrutinee
- What to check first:
  - the scrutinee type
  - the pattern kind at the reported span
- Usual class:
  - typing issue

### `E107` - semantic call target is not callable

- Short meaning:
  - the current MVP rejected the call target itself
- Typical cause:
  - calling a local value as if it were a callable
  - calling a boolean literal as if it were a callable
  - using a non-identifier call target in MVP
- What to check first:
  - the callee expression itself
  - whether the callee is a builtin identifier, unresolved external identifier, or a local non-callable value
- Usual class:
  - callable/use-shape issue

## Parser / Validation / Golden Distinction

Keep these failure modes separate.

### Parser / Earlier Validation Rejection

Typical signs:

- codes outside `E100`-`E107`
- malformed source
- invalid token/character
- delimiter or structure problems

Representative current examples:

- `E010` unexpected character
- `E021` unclosed delimiter / delimiter-shape failure
- `E023` invalid `let` structure

Meaning:

- the input was not accepted by the frontend
- static semantics may not have run yet

### Semantic Rejection

Typical signs:

- codes `E100`-`E107`
- input parsed, but current shipped semantic checks rejected it

Meaning:

- the validator accepted the syntax far enough to perform current static-semantics checks
- the rejection is about current validator constraints, not just malformed syntax

### Golden Mismatch

Typical signs:

- `golden canonical mismatch`
- `golden hash mismatch`
- `golden error code mismatch`
- `golden error message class mismatch`
- `golden exact span mismatch`

Meaning:

- the fixture expectation did not match actual validator behavior
- the source may still be valid or invalid exactly as designed; the problem is the conformance expectation mismatch

## Common Operator Mistakes

### Wrong file path

- `canon` fails because the input file path is wrong
- check the path before assuming validator failure

### Wrong fixture path

- `golden` fails because the fixture file does not exist or the wrong fixture corpus was used
- check the exact fixture path first

### Malformed source

- parser/earlier rejection appears before semantic checks
- look for non-`E100`-`E107` codes such as lexer/parser failures

### Semantic rejection

- source parses, then current semantic checks reject it
- use the `E100`-`E107` table above before guessing

### Using the wrong fixture corpus

- shipped demo fixtures and project-owned fixtures are not interchangeable unless intended
- confirm which corpus the command was supposed to use

### Reading a `golden` mismatch as "the platform is broken"

- a `golden` mismatch is usually a conformance expectation mismatch, not proof of runtime/backend/platform failure
- keep the interpretation narrow and validator-first

## What To Capture When Reporting An Issue

Capture exactly:

- exact command
- exact input file or fixture file
- exact output
- exact diagnostic code and span if present
- validator version / release tag

For the current shipped cut, the release tag is:

- `stage1-tobi-validator-v0.7.0`

Support-quality rule:

- prefer minimal reproducible inputs
- prefer exact fixture files over paraphrases
- include whether this was `canon` or `golden`
- include whether the issue is docs mismatch, diagnostics clarity, fixture mismatch, or workflow friction

## Non-Goals

This document does not:

- define Tsubasa semantics
- replace release docs
- promise runtime behavior
- promise backend/materialization behavior
- promise verification API behavior
- widen the shipped product into a broader platform

Later enhancement / not part of first shipped diagnostics/reference UX:

- richer diagnostic cookbook by syntax family
- platform-specific onboarding
- API-oriented error handling guidance
