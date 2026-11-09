---
name: design-system-refactor
description: "Refactor a frontend design system with zero visual change: tokens, shared components, guardrails, in any framework. Use when the user asks to refactor or clean up a design system, theme, tokens or component library, or to remove hardcoded styles and duplicated UI."
---

# Design system refactor

A refactor changes the code and keeps the result pixel-identical: same pixels, focus rings, keyboard paths and accessible names. Design improvements become notes for the user. Aim for the smallest change that meets the intent.

## Modes

Pick the mode from the request. With no mode named, run them in this order.

| Mode | Does | Done when | Read |
| --- | --- | --- | --- |
| interview | Settles every decision before any edit | No open branch would change an edit | [references/interview.md](references/interview.md) |
| audit | Read-only inventory of values, duplicates and drift | Every literal value and every 3+ repetition is listed with its files | Audit, below |
| tokens | Moves values into one token source and its DESIGN.md mirror | The area has no literal design value outside the token file, except one-off geometry | [references/tokens.md](references/tokens.md) |
| extract | Turns repeated UI into shared components | Every call site in the area uses the component | Extract, below |
| guard | Adds checks that keep the system from drifting | Every check is enabled and passes | [references/guardrails.md](references/guardrails.md) |

## Rules for every mode

- Before deciding anything, read `DESIGN.md`, the theme or token files and two neighboring components. Match their naming, file layout and export style.
- Work one area at a time. An area is a route, feature folder or component family. Convert every call site in it, verify, then commit.
- Run the project's lint, typecheck, tests and build before the first edit (the baseline) and after each area. Each area ends green.
- Each area ends with the visual check at 0 pixels of difference.
- Hand heavy reading and each area's edits to fresh-context helper agents, one writing helper at a time. Give each helper the interview decisions, the area's file list and the pixel-identical rule. The main session coordinates and verifies.

## Audit

Run as a read-only helper. Collect:

1. Every literal design value (color, spacing, font size, weight, line height, radius, shadow, z-index, duration, easing, breakpoint) with its count and files.
2. Drift: groups of near-identical values (`#cfcfcf` and `#d0d0d0`, `13px` and `0.8125rem`). Drift values stay distinct, since merging them changes pixels; report them for a later design pass.
3. Markup or class strings repeated 3 or more times.
4. Several implementations of one concept (three button styles, two card shells).
5. Library primitives (shadcn, Radix, MUI and similar) copied and edited in place.

Hand the inventory to the main session with a proposed area order: shared foundations first, then the areas with the most repetition.

## Extract

- Extract what appears 3 or more times; two copies stay inline.
- Name each component after its job in the product: `InvoiceRow`, `PlanCard`.
- Wrap library primitives in local components or variants, leaving upstream files as they are.
- The component renders the exact markup, classes and attributes each call site rendered before. Where call sites differ, expose the difference as a prop or variant.
- Keep accessible names, roles, `aria-*` attributes, tab order and event handlers identical.
- Update every call site in the area in the same change.

## Visual check

For each route in the area, before the first edit and after the last:

1. Capture screenshots at 1440 px and 390 px wide, in light and dark themes when the project has both, plus hover and focus states of the touched components. Use the project's visual test runner when one exists; otherwise the built-in browser or `bunx playwright screenshot`.
2. Compare each pair pixel by pixel, for example `bunx pixelmatch before.png after.png diff.png 0`. The check passes at 0 different pixels.
3. Compare the accessibility tree and tab order of the touched components.

On a difference, find the edit that caused it, fix it and check again. After 3 failed rounds, revert the area and report the cause.

## Final report

When all areas are done, report four scores from 1 to 10, each with one line of measured before and after counts:

- Logic: clarity of the code structure (duplicate implementations removed, clear component APIs).
- Design quality: consistency of the system (share of values served by tokens, one-offs left).
- Essence: how few, meaningful tokens and components now carry the product's look.
- Shortening: code removed (lines, repeated class strings, files).

Then list, one line each, the drift values and design issues left for the user.

Inspired by Matt Pocock's skills and their community variants (moduo-design-quality, design-help), impeccable's extract, shadcn's skill and the Tailwind v4 refactor skills.
