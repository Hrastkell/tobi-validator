---
name: Workflow fit discussion
about: Ask a concrete GitHub-first workflow-fit question for the released Stage 1 line
title: "[workflow-fit] "
labels: workflow-fit
assignees: ''
---

# Workflow fit discussion

Use this template for a **concrete workflow-fit question** related to the
currently released Stage 1 line of:

**AI Verification Engine / Tobi Validator**

The current public launch motion is GitHub-first.

Use this template when you want to discuss:
- where the validator fits in a GitHub workflow
- how to think about `canon` and `golden` in CI
- how a narrow validator gate should sit inside a repository workflow

Do not use this template to assume that the following are already active public
launch channels:
- GitLab
- Nextflow
- Snakemake
- broader platform/runtime/backend/API surfaces

## 1. Workflow summary

Describe your workflow in one or two direct sentences.

## 2. What you are trying to accomplish

Examples:
- gate reasoning artifacts before merge
- compare canonical outputs across runs
- use `golden` as a reproducibility-oriented check
- understand whether the released CLI fits a narrow CI gate

## 3. Current environment

Fill in what is relevant:

- GitHub repository type:
- local or CI usage:
- expected trigger:
  - [ ] pull request
  - [ ] push
  - [ ] release
  - [ ] other
- operating environment:
- current workflow tooling:

## 4. Current question

State the concrete question clearly.

Examples:
- where should `canon` run in this workflow?
- where should `golden` run in this workflow?
- should this be a pull-request gate or a release gate?
- does this fit the current released Stage 1 surface?

## 5. Relevant command / draft workflow

If you already have a command or workflow draft, paste it here.

```yaml
paste workflow or command here
```

## 6. What kind of answer you need

Choose what would help most:

- [ ] placement guidance
- [ ] docs clarification
- [ ] starter workflow interpretation
- [ ] understanding product scope
- [ ] determining whether this is in current Stage 1 fit
- [ ] other narrow workflow-fit guidance

## 7. Scope confirmation

Please confirm:

- [ ] I understand the current public launch motion is GitHub-first
- [ ] I am not treating later workflow channels as already active public launch paths
- [ ] I am asking about narrow workflow fit around the released validator CLI
