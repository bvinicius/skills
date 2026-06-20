# bvinicius/skills

A Claude Code plugin marketplace for dev workflow skills — bug-fixing, triage, and more.

## Install

```
/plugin marketplace add bvinicius/skills
/plugin install dev-toolkit@bvinicius
```

Skills are then available as `/dev-toolkit:triage`, `/dev-toolkit:bug-fix`, etc.

## Plugins

| Plugin | Description |
|--------|-------------|
| [dev-toolkit](./plugins/dev-toolkit) | Bug-fixing, triage, and related dev workflow skills |

## Adding a new plugin

1. Create `plugins/<plugin-name>/` with `.claude-plugin/plugin.json` and a `skills/` directory.
2. Add one entry to `.claude-plugin/marketplace.json` under `plugins`.
3. Push — users can then `/plugin install <plugin-name>@bvinicius`.

See [dev-toolkit/README.md](./plugins/dev-toolkit/README.md) for the skill authoring guide.
