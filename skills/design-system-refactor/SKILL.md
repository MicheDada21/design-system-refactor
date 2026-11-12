---
name: design-system-refactor
description: "Moves hardcoded styles into tokens and repeated UI into shared components, preserving appearance, behavior and accessibility. Use when cleaning up a design system, theme or component library in any framework."
---

# Design system refactor

A refactor changes the code while preserving the visible design, focus states, keyboard paths and accessible names. Design improvements become notes for the user unless separately requested. Aim for the smallest change that meets the intent.

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
- Work one area at a time. An area is a route, feature folder or component family. Convert every call site in it and verify before starting the next; follow the project's delivery policy for commits.
- Establish a baseline with the project's existing lint, typecheck, test and build commands. Rerun relevant checks after each area; report unavailable or skipped checks.
- Each area ends with checks for meaningful visual regressions and unchanged interaction and accessibility, within the project's authorized verification workflow.
- When delegation is available and authorized, hand heavy reading and each area's edits to fresh-context helper agents, one writing helper at a time. Give each helper the interview decisions, the area's file list and the preservation rule. The main session coordinates and verifies.

## Audit

Run as a read-only helper. Collect:

1. Every literal design value (color, spacing, font size, weight, line height, radius, shadow, z-index, duration, easing, breakpoint) with its count and files.
2. Drift: groups of near-identical values (`#cfcfcf` and `#d0d0d0`, `13px` and `0.8125rem`). Keep drift values distinct during the refactor; report possible consolidation for a later design pass.
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

Follow the user's and project's browser policy. When browser checks are authorized, reuse the project's runner or browser tooling and compare representative routes before and after at desktop and mobile widths. Include supported themes and touched hover, focus and open states where relevant. Wait for fonts, images and motion to settle.

Judge whether layout, spacing, typography, colors, imagery and responsive behavior remain visually equivalent. Use pixel diffs to locate suspicious changes when useful; a nonzero count alone is not a failure. Ignore harmless antialiasing, subpixel rounding and image-rasterization noise when the rendered design and relevant computed styles agree. No universal pixel threshold is required.

Check the touched controls' accessible names, roles, states, focus visibility and keyboard order, using accessibility snapshots or focused interaction checks when available.

Pass the refactor when no unintended visible changes remain and touched controls retain their behavior and accessibility. Investigate meaningful differences in the touched area and fix actual regressions. Bound diagnosis to three focused rounds; stop early when only rendering noise remains. Revert the affected change only for an unresolved functional or visible regression, and report it.

If browser checks are unavailable or disallowed, complete the permitted code and project checks and state that visual equivalence was not directly verified.

## Final report

When all areas are done, report four scores from 1 to 10, each with one line of measured before and after counts:

- Logic: clarity of the code structure (duplicate implementations removed, clear component APIs).
- Design quality: consistency of the system (share of values served by tokens, one-offs left).
- Essence: how few, meaningful tokens and components now carry the product's look.
- Shortening: code removed (lines, repeated class strings, files).

Then list, one line each, the drift values and design issues left for the user.

Inspired by Matt Pocock's skills and their community variants (moduo-design-quality, design-help), impeccable's extract, shadcn's skill and the Tailwind v4 refactor skills.
