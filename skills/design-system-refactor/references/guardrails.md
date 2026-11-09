# Guardrails

Add these after the last area passes, so the system stays clean. Each check must pass on the refactored code before it is enabled.

## Automatic checks

Wire them into the project's existing lint script and CI.

- Raw values: flag hex, rgb, hsl and oklch colors, and px or rem sizes, outside the token stylesheet. Use Stylelint for CSS (`color-no-hex`, `declaration-property-value-disallowed-list`) and the project's linter for markup and class strings.
- Arbitrary utilities: in Tailwind, flag arbitrary values such as `text-[13px]` or `bg-[#fff]`, while allowing `[var(--token)]` and one-off geometry.
- Inline styles: flag static `style` props that set color, spacing or type.
- Mirror sync: a small script fails when a token in the stylesheet is missing from `DESIGN.md` or the reverse.

When a check fires, its message names the nearest existing token.

## Review pass

What a regex cannot see. Run it as a fresh-context helper on each future change to UI files:

- A new component that duplicates an existing one.
- A library primitive edited in place instead of wrapped.
- A semantic token used for the wrong role (an accent color used as decoration).
- A new literal value that should have become a token.

The review reports findings and changes nothing.
