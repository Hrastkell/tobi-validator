# Stage 1 Install And Usage

Project: Organetic Sphere  
Component: Tobi  
Product: AI Verification Engine / Tobi Validator  
Scope: install / usage / output interpretation  
Date basis: 2026-03-29

For the shortest first-time path from download to a successful `canon` and
`golden` run, start with:

- `docs/STAGE1_QUICKSTART_FIRST_10_MINUTES.md`

## Install

First-cut install flow:

1. Download `stage1-tobi-validator-v0.7.0-windows-x86_64.zip`.
2. Verify it against `stage1-tobi-validator-v0.7.0-windows-x86_64.zip.sha256`.
3. Unpack `stage1-tobi-validator-v0.7.0-windows-x86_64.zip`.
4. Keep the extracted directory intact so both `examples/sample.tsubasa` and
   `examples/golden/fixtures.json` remain available.
5. Keep the bundle-internal `SHA256SUMS.txt` with the unpacked files for local integrity verification.
6. Run `tobi.exe --help` from the extracted directory.
7. Optionally add the extracted directory to `PATH`.

The help banner should identify the released product line as:

- `AI Verification Engine / Tobi Validator`

## Canon Usage

Example:

```powershell
.\tobi.exe canon .\examples\sample.tsubasa
```

This sample is shipped inside the release bundle.

Expected output shape:

- `CANON:` section with canonical ASCII
- `HASH:` section with the current `_h` value rendered as hex

## Golden Usage

Example:

```powershell
.\tobi.exe golden .\examples\golden\fixtures.json
```

This fixture file is shipped inside the release bundle.

Expected output shape:

- `OK (<n> fixtures)` on success
- deterministic diagnostic/conformance failure on mismatch

## Output Interpretation

### Canonical ASCII

Canonical ASCII is the stable user-visible normalized form of accepted input.
Equivalent source skins should converge here.

### Hash

`HASH` is the current user-visible `_h` surface for the accepted canonical artifact.

### Diagnostics

Rejected input produces deterministic diagnostics with stable error codes and spans under the current validator contract.

## Compatibility And Conformance Note

This first shipped cut is validator-first.
It is intended for canonicalization, validation, diagnostics, and conformance work.

It is not intended for:

- runtime execution
- backend emission
- verification API integration
- broader SDK/platform embedding

## Non-Goals

Do not infer from this install guide that the product already ships:

- backend-entry surface
- runtime
- codegen
- materialization
- verification API

## Where To Go Next

After install and first-run validation:

- use `docs/STAGE1_DIAGNOSTICS_REFERENCE.md` when `canon` or `golden` fails
- use `docs/STAGE1_GITHUB_ACTION_STARTER.md` if GitHub workflow fit matters
