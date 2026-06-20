# bvinicius/skills

A Claude Code plugin marketplace for dev workflow skills — bug-fixing, triage, and more.

## Install

```
/plugin marketplace add bvinicius/skills
```

Skills are then available as `/dev-toolkit:triage`, `/dev-toolkit:bug-fix`, etc.

## Plugins

| Plugin | Description |
|--------|-------------|
| [dev-toolkit](./plugins/dev-toolkit) | Bug-fixing, triage, and related dev workflow skills |
| [product-studio](./plugins/product-studio) | Product strategy and management agents for solo builders |

## Exposed resources

A plugin can ship five kinds of component. Below is what this marketplace currently exposes, grouped by type.

### Skills
Model-invoked capabilities, available as `/plugin-name:skill-name`.

| Skill | Plugin | Description |
|-------|--------|-------------|
| [bug-fix](./plugins/dev-toolkit/skills/bug-fix) | dev-toolkit | Fix a bug end to end |
| [triage](./plugins/dev-toolkit/skills/triage) | dev-toolkit | Triage an incoming issue |
| [refine-issue](./plugins/dev-toolkit/skills/refine-issue) | dev-toolkit | Sharpen a raw issue into an actionable ticket |

### Agents
Custom subagents (`agents/<name>.md`) that run in their own context window.

| Agent | Plugin | Description |
|-------|--------|-------------|
| [product-strategist](./plugins/product-studio/agents/product-strategist.md) | product-studio | Brutally honest strategy + PM sparring partner for solo builders |

### Slash commands
User-triggered fixed workflows (`commands/<name>.md`).

_None exposed yet._

### Hooks
Shell run on lifecycle events (`hooks/hooks.json`, e.g. `PreToolUse`, `PostToolUse`).

_None exposed yet._

### MCP servers
External tool servers bundled with a plugin (`.mcp.json`).

_None exposed yet._

## Adding a new plugin

1. Create `plugins/<plugin-name>/` with `.claude-plugin/plugin.json` and a `skills/` directory.
2. Add one entry to `.claude-plugin/marketplace.json` under `plugins`.
3. Push — users can then `/plugin install <plugin-name>@bvinicius`.

See [dev-toolkit/README.md](./plugins/dev-toolkit/README.md) for the skill authoring guide.
