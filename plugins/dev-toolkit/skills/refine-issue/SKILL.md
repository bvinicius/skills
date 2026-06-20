---
name: refine-issue
description: Sharpen a raw issue/ticket into a clear, actionable one — clarify intent, add acceptance criteria, surface open questions, scaled to the issue's complexity. Use when the user asks to refine, clean up, rewrite, or "make actionable" a ticket or issue before work starts.
---

# Refine issue

Turn a vague or half-formed ticket into one someone can pick up and act on, without
gold-plating it. Refine improves the *ticket* — its clarity, scope, and success
criteria — not the code. It does not decide how urgent the work is (that's
`/dev-toolkit:triage`) or implement anything (that's `/dev-toolkit:bug-fix`).

The one rule that matters most: **match the output to the issue.** A typo fix gets a
sharper one-liner, not a problem statement with acceptance criteria. Padding a simple
ticket with empty scaffolding makes it *harder* to read, not more professional.

## Workflow

1. **Understand the raw issue.** Restate the underlying goal or problem in one or two
   lines, in the reporter's terms. If you can't state it crisply, that's the first
   gap to flag — don't paper over it with confident-sounding prose.

2. **Find the gaps.** Note what's missing or unclear: ambiguous wording, absent repro
   or context, undefined "done", hidden assumptions, or several concerns tangled into
   one. These feed both the rewrite and the open-questions list.

3. **Gauge complexity — this sets the output depth.** Pick the lightest tier that
   fits:
   - **Trivial** — typo, copy tweak, obvious config or one-line change. Return a
     clean title and a one-line sharpened description. **Nothing else.** No problem
     statement, no acceptance criteria, no sections. Do not inflate it.
   - **Standard** — a normal feature or bug that needs clarifying. Give a title,
     problem/context, acceptance criteria, scope/non-goals (only if relevant), and
     open questions.
   - **Large / ambiguous** — multiple concerns bundled together, or genuinely
     unclear. Refine it as Standard, and also flag that it should probably be split,
     suggesting where the seams are.

   When you're between two tiers, choose the lighter one and say why in a line.

4. **Write the refined issue** at the chosen depth. Acceptance criteria — only when
   the tier calls for them — should be concrete and testable, not restatements of the
   title. Keep a neutral tone and preserve the reporter's intent; refine, don't
   redesign. The structure below is a ceiling, not a checklist: drop any section that
   adds no information for *this* issue.

5. **Surface open questions** as a short list the author can clear in one round trip.
   Never invent facts, scope, or requirements to fill a gap — an explicit question
   beats a confident guess.

6. **Offer to save it.** Put the refined version where the team already tracks work,
   rather than assuming:
   - If Linear MCP tools are available, offer to update the issue (or create one) in
     Linear.
   - Otherwise, if `gh` is available (check `gh auth status` / a GitHub remote),
     offer to open/update a GitHub issue.
   - If more than one is available, or you're unsure which the team uses, ask.
   - If no integration is available, output the refined ticket as paste-ready
     markdown.

## Output

**Trivial** — keep it to two lines, no fenced sections:

```markdown
**Title:** <sharpened title>
**Description:** <one-line clarified description>
```

**Standard** (and Large, plus a split note) — only include the lines that carry
information:

```markdown
## <refined title>
**Problem / context:** <why this matters, what's happening>
**Acceptance criteria:**
- <concrete, testable outcome>
- <...>
**Scope / non-goals:** <what's explicitly in or out — omit if obvious>
**Open questions:** <list the author can answer in one pass, or "none">
```

For a Large issue, add one line recommending the split and naming the pieces.
