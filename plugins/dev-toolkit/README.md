# dev-toolkit

Bug-fixing, triage, and related dev workflow skills for Claude Code.

## Skills

| Skill | Trigger |
|-------|---------|
| `/dev-toolkit:triage` | Triage a bug/issue — severity, area, reproducibility, next action |
| `/dev-toolkit:bug-fix` | Systematic root-cause fix — reproduce, locate, fix, verify, regress |
| `/dev-toolkit:refine-issue` | Sharpen a raw issue into an actionable ticket — scales depth to complexity |

## Adding a skill

1. Create `skills/<name>/SKILL.md` with a frontmatter `name` and `description`.
2. Write the steps Claude should follow in the body.
3. That's it — no manifest update needed within the plugin.
