# Keep README.md current

`README.md` has an **Exposed resources** section listing every component the marketplace exposes, grouped by type: Skills, Agents, Slash commands, Hooks, MCP servers. This list is hand-maintained — it does not auto-update.

Whenever you add, rename, or remove a component under `plugins/`, update the matching group in `README.md` in the same change:

- New `skills/<name>/SKILL.md` → add a row to **Skills**.
- New `agents/<name>.md` → add a row to **Agents**.
- New `commands/<name>.md` → add a row to **Slash commands**.
- New `hooks/hooks.json` entry → list it under **Hooks**.
- New bundled MCP server → list it under **MCP servers**.

When a group goes from empty to populated, replace its `_None exposed yet._` placeholder with a table; when it empties out, restore the placeholder. Only count components under `plugins/` — local skills under `.agents/` are not part of the marketplace and must not be listed.
