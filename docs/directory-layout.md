# Directory layout

```
plugins/<plugin-name>/
  .claude-plugin/
    plugin.json          # name, description, version, author
  config.yaml            # user preferences — fill once, all skills in the plugin read it
  README.md
  skills/
    <skill-name>/
      SKILL.md           # required — frontmatter + instructions
      scripts/           # optional executables
      references/        # optional docs / schemas
      assets/            # optional templates / UI
```

The `plugins/` directory is auto-scanned. No manifest update is needed when adding a new skill.
