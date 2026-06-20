---
name: triage
description: Triage an incoming bug or issue — assess severity, area, reproducibility, and recommend next steps. Use when the user reports a bug, pastes an error, or asks how serious/urgent an issue is.
---

# Triage

Turn a raw bug report into a clear, consistent assessment and a single concrete
next action. Triage is about *deciding what to do* — it does not fix the bug.

## Workflow

Work through these in order. The point of the sequence is to ground every
conclusion in evidence rather than a hunch.

1. **Restate the problem.** Summarize the expected vs. actual behavior in the
   reporter's terms. This catches misunderstandings early — if you can't state
   the problem crisply, you don't yet have enough to triage.

2. **Gather context.** Pull together the error/stack trace, repro steps, affected
   version or environment, and how often it happens. When key facts are missing,
   note them as gaps rather than guessing — those gaps decide whether the outcome
   is "needs-repro".

3. **Classify severity.** Pick one, since severity drives how urgent the next
   action is:
   - **blocker** — data loss, a security hole, or a core flow broken with no
     workaround.
   - **major** — an important feature is broken but a workaround exists.
   - **minor** — cosmetic, or an edge case few users hit.

4. **Identify the affected area.** Name the component, module, or `file:line`.
   When you have the codebase, use Grep/Glob to confirm where the relevant code
   lives instead of asserting blindly. If you can't pin it down, say so.

5. **Assess reproducibility.** Decide whether it reproduces **reliably**,
   **intermittently**, or **not yet**. If not yet, list exactly what's needed to
   reproduce it.

6. **Recommend a next action.** Choose one and tie it back to severity +
   reproducibility:
   - **fix now** — reproducible and severe enough to act on immediately.
   - **file issue** — real but not urgent enough to drop everything.
   - **needs-repro** — can't yet be acted on; more information is required.
   - **won't fix** — out of scope, intended behavior, or not worth the cost.

## Output

Always emit the assessment in this exact structure so reports stay scannable and
comparable:

```markdown
## Triage: <short title>
**Severity:** blocker | major | minor
**Area:** <component / file:line if known>
**Reproducible:** reliably | intermittently | not yet (missing: ...)
**Expected vs actual:** <one line each>
**Missing info:** <list, or "none">
**Next action:** <fix now | file issue | needs-repro | won't fix> — <why>
```

## Acting on the next action

- **fix now** → suggest the user run `/dev-toolkit:bug-fix` for the root-cause
  fix. Don't fix it inline here — triage stays focused on assessment, and bug-fix
  owns the reproduce → locate → fix → verify → regress loop.

- **file issue** → file it where the team already tracks work, rather than
  assuming:
  - If Linear MCP tools are available, offer to create the issue in Linear.
  - Otherwise, if `gh` is available (check with `gh auth status` / a GitHub
    remote), offer to open a GitHub issue.
  - If more than one is available, or you're unsure which the team uses, ask.
  - If no integration is available, output a ready-to-paste ticket — a title plus
    a body built from the triage report above.

- **needs-repro** → list precisely what information or steps you need to proceed,
  so the reporter can close the gap in one round trip.

- **won't fix** → state the reason plainly so the decision is on record.
