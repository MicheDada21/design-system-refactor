# Tokens

## One source, one mirror

- The source is one stylesheet of CSS custom properties (for example `src/styles/tokens.css`). Every framework can read it, so the system works with Tailwind, plain CSS, CSS modules or CSS-in-JS.
- `DESIGN.md` at the repository root mirrors it in Google's open format: YAML front matter (`name`, `colors`, `typography`, `spacing`, `rounded`, `components` with `{token.refs}`), then the sections Overview, Colors, Typography, Layout, Elevation & Depth, Shapes, Components, Do's and Don'ts. The stylesheet wins any disagreement; update the mirror in the same commit.

## Framework bridges

- Tailwind v4: expose the variables with `@theme inline { --color-surface: var(--surface); ... }` so utilities read the tokens.
- Tailwind v3: point `theme.extend` keys at `var(--token)` and plan the v4 migration as a separate task.
- CSS-in-JS: the theme object returns `var(--token)` strings, never raw values.
- Plain CSS or modules: use `var(--token)` directly.

## Values

- A token's value is the exact value the code renders today. Read computed values in the browser when the source uses math, `calc()` or inheritance.
- Each distinct rendered value gets its own primitive token, even when it looks like a near-miss. Merging values is a design change and waits for the user.
- Semantic tokens (`--text-muted`, `--surface-raised`) point at primitives. Components use semantic tokens.
- Keep the color format the code uses today. Converting hex to OKLCH can shift rendered colors.
- Theme variants override semantic tokens under the selector the project already uses (`.dark`, `[data-theme]`, `prefers-color-scheme`).

## Replacing literals

Replace a literal only when the token resolves to the identical value in every theme. Leave one-off geometry (a single `top`, `translate` or `width` used once) inline.
