---
name: bug-fix
description: Systematic root-cause bug fixing — reproduce, locate the true cause, apply a minimal fix, verify, and guard it with a regression test. Use when the user asks to fix a bug, says something is broken/crashing/erroring, pastes a stack trace and wants it resolved, or hands off a triaged "fix now" issue.
---

# Bug fix

Fix the *cause*, not the symptom, and leave behind a test that proves the bug is
dead. A fix you can't reproduce a failure for is a guess; a fix without a
regression test is one refactor away from coming back. The workflow below exists
to keep both of those from happening.

This skill owns the reproduce → locate → fix → verify → regress loop. If the
problem hasn't been assessed yet (how severe, where, is it even reproducible),
that's `/dev-toolkit:triage` — come back here once it's clear the bug is worth
fixing now.

## Workflow

Work the steps in order. Each one earns the right to the next: you can't
confidently locate a cause you can't trigger, and you can't claim a fix works if
you never had a failing case to compare against.

1. **Reproduce it first.** Before reading a line of the fix, get the failure to
   happen on demand — a failing test, a script, or a precise sequence of steps
   with the actual output captured. This is the single highest-leverage step: it
   converts "it's broken" into a concrete signal you can watch flip to green.
   Prefer writing the reproduction as an automated test from the start, because
   that same test usually becomes your regression guard in step 5.

   If you *can't* reproduce it, stop and say so rather than fixing blind. List
   exactly what you tried and what you'd need (a specific input, environment,
   data, or version). A change made against a failure you never saw can't be
   verified — flag that risk explicitly instead of pretending otherwise.

2. **Find the root cause, not the crash site.** The place an error surfaces is
   usually downstream of where it went wrong. Trace backward from the symptom:
   read the stack trace, follow the bad value to its origin, use `git blame` /
   `git log` on the suspect lines to understand when and why the code got that
   way. State the cause in one sentence before you touch anything — if you can't,
   you're still guessing, and a guarded guess is still a guess.

   Resist the pull to patch where it's convenient (a null check at the crash
   site, a `try/except` swallowing the error). That hides the symptom and leaves
   the cause live to resurface elsewhere.

3. **Apply the minimal fix at the cause.** Change as little as possible to
   correct the actual defect. A tight diff is easy to review, easy to reason
   about, and easy to revert. Don't fold in refactors, style cleanups, or
   adjacent "while I'm here" improvements — they blur what fixed the bug and
   widen the blast radius. If you spot other issues, note them separately rather
   than smuggling them into this change.

4. **Verify against the original failure.** Rerun the exact reproduction from
   step 1 and confirm it now passes. Then run the surrounding test suite (and
   linters/type checks if the project uses them) to catch anything the fix broke
   — a fix that introduces a regression isn't done. Report what you actually ran
   and its real result; if something still fails or you couldn't run a check, say
   so plainly instead of assuming.

5. **Add a regression test guarding the fix.** Leave a test that fails on the old
   code and passes on the new, so this exact bug can't silently return. Ideally
   it's the reproduction from step 1, promoted into the suite and placed next to
   related tests following the project's existing conventions. Sanity-check that
   it genuinely guards the fix: if it passes even when you revert the change, it
   isn't testing the right thing.

   If the project has no test infrastructure at all, don't scaffold one
   unprompted — say a regression test would otherwise go here and ask, or fall
   back to documenting the manual reproduction so the verification isn't lost.

## Wrapping up

Close with a short, honest summary so the change is reviewable at a glance:

```markdown
## Fix: <short title>
**Root cause:** <one sentence — the actual defect, not the symptom>
**Fix:** <what changed and where, e.g. file:line>
**Verification:** <what you ran and the result>
**Regression test:** <what now guards it — or why none was added>
```

Match the surrounding code when you edit: its naming, error-handling style, and
test conventions. A fix that reads like it was always there is easier to trust
than one that announces itself.

Commit or open a PR only if the user asks — some workflows prefer to review the
working tree first.
