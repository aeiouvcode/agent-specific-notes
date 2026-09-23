# agent-specific-notes

A field log of the mistakes that keep coming back in this build shop, what caused them, and the fix that stuck.

These notes come from real incidents across the projects on this account: games, tools and experiments built and shipped to GitHub Pages. Every entry happened at least once. Most happened more than once, which is why they are written down.

## How to use this

Start every session with [notes/working-protocol.md](notes/working-protocol.md): read the project's state files and recent commits before changing anything. Then, before you start an operation, open the file for that area and read the standing rules. It takes a minute and it is cheaper than repeating a known failure.

| About to... | Read first |
| --- | --- |
| Publish, deploy or share a link to a build | [notes/deploys-and-hosting.md](notes/deploys-and-hosting.md) |
| Drive a remote or headless browser | [notes/browser-automation.md](notes/browser-automation.md) |
| Create a repo, push files or change repo settings | [notes/github-permissions.md](notes/github-permissions.md) |
| Send a message, file or link to the owner | [notes/messaging-and-delivery.md](notes/messaging-and-delivery.md) |
| Call a build done, or grade it | [notes/qa-and-verification.md](notes/qa-and-verification.md) |
| Ship anything with network calls, user data or storage | [notes/security.md](notes/security.md) |
| Design a screen or pick a visual direction | [notes/design-rules.md](notes/design-rules.md) |
| Hit the limits of a renderer, or pick an engine or stack | [notes/engines-and-tooling.md](notes/engines-and-tooling.md) |
| Touch a token, key, password or one-time code | [notes/secret-handling.md](notes/secret-handling.md) |
| Start, resume or hand off any task | [notes/working-protocol.md](notes/working-protocol.md) |

When something goes wrong mid-task, search this repo for the symptom (an error message, a status code, a behavior) before debugging from scratch.

## Entry format

Every entry has the same five parts:

- **Mistake** - what was done
- **Symptom** - what it looked like from the outside
- **Root cause** - why it actually happened
- **Fix** - what resolved it
- **Rule** - the standing rule it became

## Templates

[templates/](templates/) holds the per-project state files (`CURRENT_TASK.md`, `CHECKPOINT.md`, `HANDOFF.md`) and a task spec with acceptance criteria and finding IDs. Copy them into a project when work on it starts.

## Adding an entry

Add a new entry when a failure costs real time, reaches the owner, or happens a second time. Put it in the matching file, keep the five-part format, and state the rule as something a future session can follow without context. If no file fits, create one and add it to the table above. Never put tokens, passwords, private addresses or personal data in an entry.

## Related

Part of a set of three: this repo is the failure log, [plan-orchestrator](https://github.com/aeiouvcode/plan-orchestrator) is the working method (agent contract, state templates, orchestration rules), and [research-archive](https://github.com/aeiouvcode/research-archive) holds the research behind each project.
