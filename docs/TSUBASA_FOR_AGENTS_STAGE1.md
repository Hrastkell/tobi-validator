# TSUBASA FOR AGENTS — STAGE 1

Status: public-safe explainer draft  
Scope: narrow guidance for agent-generated artifacts in the current Stage 1 corridor  
Product line: AI Verification Engine / Tobi Validator

## Purpose

This document explains how an agent should think about Tsubasa in the current
Stage 1 line.

It is intentionally narrow.

It does not try to teach the whole long-term language vision.
It teaches only enough to help an agent produce validator-meaningful artifacts.

## First rule

Do not treat Tsubasa as a general scripting language.

In the current Stage 1 corridor, the safe mental model is:

- Tsubasa is the semantic layer for canonical reasoning artifacts
- Tobi is the validator that checks and canonicalizes accepted source
- the current shipped surface is validator-first

That means the right agent behavior is:

- produce small explicit artifacts
- avoid imagined runtime features
- avoid invented authoring syntax
- stay close to what the validator can actually check

## What an agent should try to produce

A good Stage 1 agent output is:

- small
- explicit
- reviewable
- narrow in scope
- suitable for pass/fail reasoning
- easy to compare against nearby sibling cases

A bad Stage 1 agent output is:

- a long essay
- policy prose with no artifact form
- pseudo-code that no validator can parse
- “smart-sounding” structure with no operational meaning

## What agents must not invent

Do **not** invent:

- regex engines
- runtime APIs
- generic byte scanners
- general string sanitation layers
- backend execution behavior
- platform features
- YAML-like or DSL-like wrappers and call them Tsubasa
- broad language rules that current Stage 1 does not expose

If you are unsure, narrow the artifact instead of broadening it.

## A better mental model

The agent should think in terms of:

- accepted case
- rejected sibling
- canonical convergence family
- validator-facing boundary
- smallest useful case set

This is better than thinking in terms of:
- “feature-rich language program”
- “mini runtime”
- “generic parser DSL”
- “policy file pretending to be code”

## Good first authoring pattern

A good first agent-generated family looks like this:

### Accepted case
A small valid binding or artifact.

### Accepted variant
A different surface spelling that should converge to the same canonical meaning.

### Reject sibling
A nearby malformed or noisy case that should be rejected.

That is enough for a useful first validator-facing experiment.

## Two concrete patterns

### Pattern 1 — boundary
Use when the question is:
- does this kind of input pass or fail?

Shape:
- one accepted case
- one malformed reject
- one confusable/noisy reject if relevant

### Pattern 2 — convergence
Use when the question is:
- do these distinct spellings converge to one canonical result?

Shape:
- baseline accepted form
- alternate accepted spelling
- stress spelling
- malformed sibling

## How agents should move from raw output to Tsubasa-ready form

### Step 1 — start with the claim
Example:
- “this form should pass”
- “this malformed sibling should fail”
- “these two spellings should converge”

### Step 2 — strip unsupported mechanism
Remove:
- invented regex rules
- runtime assumptions
- non-existent APIs
- pseudo metadata wrappers

### Step 3 — reduce to explicit cases
Write actual cases, not commentary pretending to be executable structure.

### Step 4 — keep only validator-meaningful expectations
For example:
- should pass
- should reject
- should converge to same canonical output
- should keep stable compatibility identity when exposed

### Step 5 — save the smallest useful set
Do not start with 50 cases.
Start with 3–7.

## What belongs in canon thinking

Canon-oriented thinking should focus on:

- exact accepted source
- exact rejected source
- canonical output for accepted source
- stable comparison between accepted equivalents
- no canonical output for rejected source

## What belongs in golden thinking

Golden-oriented thinking can be a little more explanatory.

Good golden sets may include:

- baseline accepted case
- readable accepted variant
- stress spelling
- malformed nearby sibling

Golden should stay readable.
It should not pretend commentary is executable syntax.

## What agents should optimize for

Optimize for:

- explicitness
- narrowness
- comparability
- repeatability
- operational usefulness

Do not optimize for:

- expressive overreach
- pseudo-language design
- broad future-looking semantics
- sounding impressive

## A compact self-check for agents

Before finalizing an artifact, ask:

1. Can the validator actually check this?
2. Did I invent any runtime or API?
3. Did I write actual cases, or just policy prose?
4. Is there a nearby reject sibling?
5. Is the artifact small enough to reuse in CI or a workflow gate?

If the answer to question 2 is “yes”, rewrite and narrow.

## Bottom line

In Stage 1, the winning move is not to generate more language.

The winning move is to generate less noise.

A good agent-generated Tsubasa artifact is small, explicit, and validator-meaningful.
That is enough to start.
