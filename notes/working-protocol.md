# Working protocol

How a session should start, run and hand off. These rules exist because each of the failures below happened, or nearly did, when several builds ran in parallel over several days.

## Resuming from memory instead of from the repo

- **Mistake:** Picking up a project from what the last conversation said about it.
- **Symptom:** Work already done was redone, a fix already rejected was tried again, and a build regressed to an older approach.
- **Root cause:** Conversation memory is lossy and goes stale. The repo is the only state that is always current.
- **Fix:** Keep three state files in each active project (templates in [templates/](../templates/)):
  - `CURRENT_TASK.md` - the one task in progress, its acceptance criteria and its non-goals
  - `CHECKPOINT.md` - completed atomic steps, so nothing gets redone
  - `HANDOFF.md` - where to resume, what is blocked, and **failed approaches with the reason each failed**
- **Rule:** Start from repository state, not conversation memory. Update the checkpoint after each meaningful step and the handoff before stopping.

## Editing without looking at what changed

- **Mistake (near miss):** Pushing a README update to a repo that another job had committed to minutes earlier.
- **Root cause:** Several jobs work on the same account at once.
- **Fix:** Read in this order before touching anything:
  1. The project README and state files
  2. `git status` and `git log --oneline -10`, or the latest commits through the API
  3. The files you are about to change, at their current version
- **Rule:** Build every commit on the current head and update the branch without force. If the update is rejected, re-read and rebase. Never overwrite.

## Guessing how an unstable API behaves

- **Mistake:** Assuming an endpoint, permission or widget works the way it usually does.
- **Symptom:** 403s on repo settings with a contents-only token, hosted model keys that turned out to be browser-blocked by CORS, a form field that saved the autocomplete suggestion instead of the typed value.
- **Root cause:** Behavior was assumed, not observed.
- **Fix:** Before building on it, write the smallest probe that proves the behavior: one API call, a one-token completion, one saved field read back.
- **Rule:** Never invent API behavior. If it is uncertain, probe it and record the result in the handoff.

## Scope creep

- **Mistake:** Adding features the brief did not ask for, such as engagement mechanics in an app where they were not wanted.
- **Symptom:** More to review, more to break, and the owner had to ask for things to be taken out.
- **Fix:** Every task spec lists non-goals explicitly next to its goals.
- **Rule:** If it is not in the task, it is a non-goal until the owner says otherwise. Suggest it; do not build it.

## Calling it done too early

- **Mistake:** Reporting completion when the code was written but not verified.
- **Fix:** Each project has a definition of done. For a web build on this account it is:
  - [ ] Runs locally with no console errors
  - [ ] Pushed; the live Pages URL serves the new file (hash matches)
  - [ ] Checked by screenshot at desktop width and at 390px
  - [ ] Security checks pass (see [security.md](security.md))
  - [ ] `git diff` / commit diff reviewed line by line for stray changes, debug code and secrets
  - [ ] Checkpoint and handoff updated
- **Rule:** A task is complete only when every item has evidence. "Should work" is not evidence.

## The builder grading their own work

- **Mistake:** The same pass that built a feature also judged it.
- **Symptom:** Friendly grades that did not survive a side-by-side with the reference.
- **Fix:** Separate the roles. The implementer builds. A reviewer pass works adversarially: it compares against the reference, hunts for failures and files findings. The implementer fixes and the reviewer re-checks.
- **Rule:** Nobody signs off their own work. Findings come from a pass whose job is to find problems.

## Parallel jobs on one repo

- **Mistake risk:** Two jobs editing the same repository at the same time.
- **Fix:** Give each job its own branch or git worktree, and merge through a reviewed change. When committing through the API, create the commit on the current head and update the ref without force, so a conflicting update fails loudly instead of overwriting.
- **Rule:** One writer per branch. Parallel work means separate branches or worktrees.

## Vague tasks

- **Mistake:** Starting from a one-line ask with no acceptance criteria.
- **Symptom:** Loops of "not what I meant".
- **Fix:** Write a task spec before building ([templates/TASK_SPEC.md](../templates/TASK_SPEC.md)): goal, acceptance criteria, non-goals, references, and findings with stable IDs (F-01, F-02...) that commits and reviews can cite.
- **Rule:** No acceptance criteria, no start. Cite finding IDs in commit messages so every fix traces back to what it fixes.
