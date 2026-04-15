# Stage 1 Support And Issue Reporting

Project: Organetic Sphere  
Component: Tobi  
Product: AI Verification Engine / Tobi Validator  
Scope: public Stage 1 support and issue-reporting guidance  
Date basis: 2026-04-14

## What This Document Is

This document explains how to report problems and workflow-fit friction for the
currently released Stage 1 line of:

- `AI Verification Engine / Tobi Validator`

The current public launch motion is GitHub-first.

This document is for:

- reproducible bug reports
- diagnostics-oriented failure reporting
- workflow-fit questions grounded in the released validator CLI
- docs clarification requests

This document is not a promise of:

- runtime/backend support
- verification API support
- broader platform support
- automatic support for later workflow channels as already active public launch paths

## Current Released Stage 1 Surface

Keep reports narrowly grounded in the currently released surface:

- installable `tobi` CLI
- canonical ASCII output
- current `_h` compatibility identity
- deterministic diagnostics
- `golden` conformance execution
- thin packaging and install / usage framing

## Start Here Before Reporting

Before opening an issue, first check:

- `docs/STAGE1_QUICKSTART_FIRST_10_MINUTES.md`
- `docs/STAGE1_INSTALL_AND_USAGE.md`
- `docs/STAGE1_DIAGNOSTICS_REFERENCE.md`
- `docs/STAGE1_GITHUB_ACTION_STARTER.md`

If your question is about where the validator fits in a GitHub workflow, use the
workflow-fit issue template rather than a generic bug report.

## What To Report

Appropriate public reports include:

- a command that failed unexpectedly
- a diagnostics message that is unclear
- a fixture mismatch in `golden`
- docs wording that does not match observed released behavior
- a narrow GitHub workflow-fit question around the released validator CLI

## What Not To Report As If Already Released

Do not file support requests as if the following are already part of the
released public surface:

- runtime execution
- backend execution
- verification API
- platform SDK
- broad GitLab / Nextflow / Snakemake rollout
- broader Organetic platform availability

Those are outside the current Stage 1 public reading.

## How To Write A Good Bug Report

A useful bug report should include:

- exact release version / tag
- exact command run
- exact file or fixture used
- exact observed output
- expected behavior
- actual behavior
- diagnostic code and span if present
- whether the issue is reproducible

Good reports are concrete.
Vague reports create noise and slow support.

## How To Write A Good Workflow-Fit Question

A useful workflow-fit question should include:

- what workflow you are trying to support
- whether this is local or GitHub CI usage
- where you think `canon` or `golden` might belong
- what is unclear in the current docs or starter materials
- whether you are asking about current Stage 1 fit rather than future channels

## Recommended Issue Paths

Use:

- `Bug report` for reproducible Stage 1 issues
- `Workflow fit discussion` for GitHub-first workflow-fit questions

If the matter is security-sensitive, do not open a detailed public issue.
Use the private contact path described in:

- `SECURITY.md`

## Scope Reminder

This repository is the public GitHub distribution surface for the released Stage 1 line.

It is not the full development source repository.

Reports should stay grounded in the public distribution surface:
- docs
- examples
- released binaries
- workflow adoption materials

## Current Bottom Line

Use public issues for:

- reproducible released Stage 1 problems
- diagnostics questions
- docs mismatches
- GitHub-first workflow-fit questions

Do not use public issues to treat unreleased runtime/backend/API/platform
surfaces as if they were already part of the public Stage 1 product.

In short:

- keep reports narrow
- keep reports exact
- keep reports reproducible
- keep workflow-fit questions GitHub-first
