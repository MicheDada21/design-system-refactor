# Interview

Settle every decision before the first edit. Walk the decision tree branch by branch, resolving the choices other choices depend on first.

## How to ask

- Read the code first and never ask what the repository already answers. State what you found and ask only to confirm when a finding is ambiguous.
- Ask through the client's question widget, up to 4 closed questions per round, each with a concrete recommended option first and room for a free-text answer. With no widget, use a short numbered list in the same shape.
- After each round, show which branches the answers closed and which they opened. Stop when no open branch would change an edit.

## Branches to cover

1. Scope: which areas are in, which are frozen, and the area order proposed by the audit.
2. Token source: where tokens live today, if anywhere, and which file becomes the single source (see tokens.md).
3. Naming: token tiers (primitive, semantic, component) and the naming style to follow.
4. Themes: light, dark, brand or density variants that tokens must carry.
5. Component library: which primitives come from a library and must be wrapped, not edited.
6. Drift: confirm that near-identical values stay distinct during the refactor, and whether the user wants a later, separate design pass to merge them.
7. Checks: which lint, typecheck, test and visual tools the project already runs, and which ones the guard mode may add.
8. Delivery: commit cadence per area and any branch or deploy rule in the project's `AGENTS.md`.
