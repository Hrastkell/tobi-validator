# Stage 1 Quickstart - First 10 Minutes

Project: Organetic Sphere  
Component: Tobi  
Product: AI Verification Engine / Tobi Validator  
Scope: first-time public GitHub entry quickstart  
Date basis: 2026-04-15

## What This Product Is

`AI Verification Engine / Tobi Validator` is a narrow validator-first CLI.

It is for:

- canonicalizing accepted Tsubasa source
- producing the current validator-facing `_h` compatibility identity
- surfacing deterministic diagnostics
- running shipped golden/conformance checks

It is not:

- a runtime
- a backend
- a verification API
- a platform SDK

## What This Public Repository Is For

This public repository is for:

- understanding the released Stage 1 surface
- reading the public docs
- inspecting shipped examples
- understanding GitHub workflow fit
- reporting reproducible issues and workflow-fit questions

It is not the full private development source repository.

It should also not be read as an unrestricted public full-binary distribution
path for the complete Stage 1 product usage contour.

## First 10 Minutes In This Repository

Use these first 10 minutes to do four things:

1. understand the released Stage 1 product contour
2. inspect the shipped examples
3. understand the command shapes of the released CLI
4. understand the GitHub-first workflow path

## Released Command Shapes

Representative command shapes for the released validator line are:

```powershell
.\tobi.exe canon .\examples\sample.tsubasa
.\tobi.exe golden .\examples\golden\fixtures.json
```

These command shapes show how the released validator line is intended to be used.

They do not by themselves imply unrestricted public full-binary delivery through
this repository.

## Shipped Examples In This Repository

This public repository includes:

- `examples/sample.tsubasa`
- `examples/golden/fixtures.json`

Use them to understand:

- the shape of accepted input
- the shape of expected canonical output
- the kind of fixtures used by `golden`

## What Successful Stage 1 Output Looks Like

For `canon`, the expected output shape is:

- `CANON:`
- canonical ASCII body
- `HASH:`
- current `_h` rendered as hex

For `golden`, the expected output shape is:

- `OK (<n> fixtures)`

For the current shipped fixture corpus, the representative success reading is:

- `OK (45 fixtures)`

## How To Read The Output

### Canonical ASCII

Canonical ASCII is the stable user-visible normalized form of accepted Tsubasa source.
Different source skins that mean the same thing should converge here.

### HASH

`HASH` is the current validator-facing `_h` compatibility identity for the
accepted canonical artifact.

### Diagnostics

If input is rejected, Tobi returns deterministic diagnostics.

That means:

- stable error codes
- stable spans under the current validator contract
- explicit failure instead of silent acceptance

## What This First Release Does Not Do

This first shipped cut does not provide:

- runtime execution
- backend output
- code generation
- materialization
- verification API
- broader platform or integration surface

Do not read the public repository or its examples as proof of unrestricted
runtime/backend/product maturity beyond the validator-first contour.

## What To Do Next

After this first 10-minute pass through the public repository:

- read `docs/STAGE1_INSTALL_AND_USAGE.md`
- read `docs/STAGE1_DIAGNOSTICS_REFERENCE.md`
- read `docs/STAGE1_SUPPORT_AND_ISSUE_REPORTING.md`
- read `docs/STAGE1_GITHUB_ACTION_STARTER.md`

If your main question is GitHub workflow fit, the next document is:

- `docs/STAGE1_GITHUB_ACTION_STARTER.md`

If your main question is failure interpretation or issue reporting, the next
documents are:

- `docs/STAGE1_DIAGNOSTICS_REFERENCE.md`
- `docs/STAGE1_SUPPORT_AND_ISSUE_REPORTING.md`
