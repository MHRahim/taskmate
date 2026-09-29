# AGENTS.md

## Approval workflow (mandatory)

1. **No action without a plan.** Before making ANY change (editing files, creating/deleting
   files, running build/test/lint commands, installing dependencies, running migrations,
   committing, pushing, touching config), you must first write out a step-by-step plan and
   present it to the user.
2. **Wait for explicit approval.** Do not start executing until the user has explicitly
   approved the plan (or the specific step). "Ok", "go ahead", or equivalent must come from
   the user in response to the plan you presented.
3. **Approve each step individually.** Present the plan as discrete, numbered steps. After
   finishing a step, report what was done and stop, then propose the next step and wait for
   approval again. Never batch multiple steps into one unapproved action.
4. **Ask, don't assume.** If a step is ambiguous or there are multiple reasonable approaches,
   present the options and let the user choose before proceeding.

## Revertability (mandatory)

1. **Every step must be reversible.** Before executing a step, state exactly how it will be
   reverted (e.g. `git checkout -- <file>`, `git revert <sha>`, restoring a saved backup,
   dropping the created file, undoing the command).
2. **Keep a rollback record.** Maintain a running list of: step number, what changed, and the
   exact revert command/operation. Append it to the plan as you go.
3. **Be ready to revert on request.** If the user says "revert", "undo", or "roll back", stop
   all work immediately and revert the requested step(s) (or all of them) using the recorded
   operations, then report the result.
4. **Verify the revert.** After reverting, confirm the working tree / system is back in the
   prior state (e.g. `git status`, `git diff`) and report it.

## Before the first change

- Capture a baseline first: run `git status` and `git stash list` (if relevant) and note the
  current state, so any revert can be validated against it.
- Never commit or push unless the user explicitly asks for it as its own approved step.
