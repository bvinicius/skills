# Creating a plugin or skill

Run `/skill-creator`. It handles scaffolding — writes the `SKILL.md`, generates the `config.yaml` template with the keys the new skill needs, and optionally sets up test cases.

When adding a skill to an existing plugin:
1. Create `plugins/<plugin-name>/skills/<skill-name>/SKILL.md`
2. Add any new config keys the skill needs to `plugins/<plugin-name>/config.yaml` (with comments)
