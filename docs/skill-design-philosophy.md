# Skill design philosophy

These skills are personal. They're for me, used across my own projects — so they're allowed to be opinionated and to encode my values, conventions, and the way I like to work. The aim is not a vendor-neutral toolkit a stranger could drop in; it's a toolkit *I* can reuse across *my* projects.

That still means avoiding hard-coded, per-project identifiers — because they change from one of my projects to the next, not because some hypothetical stranger needs them parameterized.

## Don't hard-code what varies between my projects

Skills should not bake in things that differ across my projects: repo names, specific tracker URLs, project-specific branch names, API endpoints. Those belong in config so the same skill works in every project. Reference config keys instead.

Bad: "File a ticket in the `acme-web` Linear team"
Good: "File a ticket in the tracker configured at `ticket_tracker` in `config.yaml`"

Where I have a genuine preference (a workflow, a convention, a default tool I always reach for), bake it in. That's the point — these skills carry my opinions. Only parameterize what actually changes between projects.

## Parameterizable via per-plugin config.yaml

Each plugin ships a `config.yaml` at its root. This file captures everything that varies between my projects or environments. Fill it out once per project when you install the plugin.

Example:
```yaml
# plugins/dev-toolkit/config.yaml
ticket_tracker: linear        # linear | github-issues | jira | notion
repo_host: github             # github | gitlab | bitbucket
default_branch: main
severity_thresholds:
  critical: production_down
  high: data_loss
```

**Rules for skill authors:**
- Read `config.yaml` early in your skill's workflow and extract the keys you need
- Any value that could differ between my projects belongs in `config.yaml`, not inline
- If a key is absent, fall back to a sensible default or ask the user once — never silently do the wrong thing
- Document every recognized config key in a `## Configuration` section in your `SKILL.md`

**skill-creator integration:** When you tell skill-creator that a skill needs user preferences, it prompts you for the required config keys and adds them (with comments) to the plugin's `config.yaml` template. Existing keys are preserved.

## Reusable across my projects

Write skills so they work in any of my projects, not just the one I'm in right now. Keep per-project specifics (repo names, team names, "this stack" assumptions) out of the skill body and in config. The opinions can stay; the project-specific details move out.
