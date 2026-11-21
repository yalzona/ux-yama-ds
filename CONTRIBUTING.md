# Contributing

Figma (Yama-DS) is the source of truth. This repo is the written, machine-readable copy that Claude Design and other tools consume. Keep them in step.

## Workflow

1. Make the change in Figma first (variables, styles or components).
2. Create a branch: `git checkout -b <short-description>`.
3. Update `tokens.json` for any value changes and the matching section of `README.md` for any rule or component change.
4. Add a line to `CHANGELOG.md` under "Unreleased" with the date, what changed and why.
5. Run `python3 scripts/validate_tokens.py` and fix any errors.
6. Open a pull request, link the Figma frame or version, and request review from a code owner.

## Rules for tokens

- Every semantic color has both `light` and `dark` values.
- Reference ramps with `{color.<ramp>.<step>}`; do not paste raw hex into a semantic token unless it is an alpha or elevation value with no ramp equivalent.
- Colors with transparency are written `#rrggbb@N%`.
- Names are camelCase in `semantic`, grouped by role (text, background, input, button, table, and so on).

## Rules for the README

- Write rules as instructions ("Use X when Y"), not descriptions.
- Anything a designer would otherwise have to guess belongs in the README: sizes, when to use which component, density, and states.
- Keep component specs in the same format: variants, sizes, tokens used, notes.

## Releases

Tag a release after meaningful changes (`v0.2.0`). Use minor versions for new tokens or components and patch versions for fixes.
