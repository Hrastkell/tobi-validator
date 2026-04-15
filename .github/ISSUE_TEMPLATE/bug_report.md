---
name: Bug report
about: Report a reproducible issue in the released Stage 1 surface
title: "[bug] "
labels: bug
assignees: ''
---

# Bug report

Use this template only for issues grounded in the currently released Stage 1
surface of:

**AI Verification Engine / Tobi Validator**

This public Stage 1 surface is intentionally narrow:

- installable `tobi` CLI
- canonical ASCII output
- current `_h` compatibility identity
- deterministic diagnostics
- `golden` conformance execution
- thin packaging and install / usage framing

Do not use this template for requests about:
- runtime/backend features
- verification API features
- broader platform features
- future workflow channels as already-owed functionality

## 1. Issue summary

Describe the problem in one or two direct sentences.

## 2. Exact command run

Paste the exact command:

```text
paste command here
```

## 3. Exact file / fixture used

State the exact file or fixture used.

Examples:
- `examples/sample.tsubasa`
- `examples/golden/fixtures.json`
- your own input file
- your own fixture file

## 4. Environment

Fill in what is relevant:

- release version / tag:
- operating system:
- shell / terminal:
- local run or workflow run:
- if workflow run, which environment:

## 5. Expected behavior

Describe what you expected to happen.

## 6. Actual behavior

Describe what actually happened.

If possible, paste exact output:

```text
paste output here
```

## 7. Diagnostics

If a diagnostic was produced, include:

- diagnostic code:
- span / location if visible:
- whether this was from `canon` or `golden`:

## 8. Reproduction

Can you reproduce it consistently?

- [ ] yes
- [ ] no
- [ ] uncertain

If yes, list the shortest reproduction steps.

## 9. Issue classification

Choose the closest classification:

- [ ] docs mismatch
- [ ] diagnostics clarity issue
- [ ] expected reject but wording unclear
- [ ] unexpected reject
- [ ] fixture mismatch
- [ ] workflow friction
- [ ] setup / operator issue
- [ ] other narrow Stage 1 issue

## 10. Scope confirmation

Please confirm:

- [ ] this report is grounded in the currently released Stage 1 surface
- [ ] this report is not asking for runtime/backend/API/platform functionality as if already released
- [ ] the information above is exact to the best of my ability
