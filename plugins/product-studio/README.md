# product-studio

Product strategy and management agents for solo builders.

## Agents

| Agent | Use it for |
|-------|------------|
| `product-strategist` | Brutally honest strategy + PM sparring partner — positioning, idea generation, prioritization, feature shaping. Reads your repo and researches the real market before advising. |

The `product-strategist` runs in its own context window. Invoke it when you want
knowledge-backed feedback on the *direction* of what you're building — not for
writing or reviewing code.

## Adding an agent

1. Create `agents/<name>.md` with frontmatter (`name`, `description`, `tools`,
   optional `model`) followed by the system prompt.
2. That's it — no manifest update needed within the plugin.
