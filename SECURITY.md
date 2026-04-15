# SECURITY

## Security reporting

If you believe you have found a security-sensitive issue related to the released
Stage 1 product line of **AI Verification Engine / Tobi Validator**, do not open
a public issue for details that would create unnecessary risk.

Instead, report it privately through the project contact path.

Current private reporting path:

- security / product contact: support@organetic.ai

## What to include

Please include:

- exact product version or release tag
- operating system / environment
- exact command run
- exact input or fixture involved
- exact observed behavior
- whether the issue affects:
  - binary distribution
  - validator execution
  - workflow usage
  - diagnostics/reporting
- steps to reproduce if available

## Scope note

This repository is the public GitHub distribution surface for the released
Stage 1 line.

Security reports should stay narrowly grounded in the currently released surface:

- installable `tobi` CLI
- canonical ASCII output
- current `_h` compatibility identity
- deterministic diagnostics
- `golden` conformance execution
- thin packaging and install / usage framing

This repository should not be read as a claim of:

- runtime/backend product surface
- verification API surface
- platform SDK surface
- broader Organetic platform release surface
