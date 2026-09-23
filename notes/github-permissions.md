# GitHub permissions

## A fine-grained token cannot create repos, enable Pages or edit settings

- **Mistake:** Using the fine-grained personal access token for every GitHub operation.
- **Symptom:** `403 Resource not accessible by personal access token` on repo creation, enabling Pages, editing the description or website, and setting topics.
- **Root cause:** The token is scoped to repository Contents (read/write) only. Creating repos, Pages and repo metadata need Administration or account-level permission, which it does not have.
- **Fix:** Push files with the token through the REST API (Git Data or Contents endpoints). Do repo creation, Pages setup and the About panel (description, website, topics) through the signed-in GitHub web session.
- **Rule:** Token for contents, signed-in web session for everything administrative. Do not retry a 403 on those endpoints hoping it passes.

## Use one commit per logical change

- **Mistake:** Pushing files one at a time through the Contents API.
- **Symptom:** Noisy history, and a half-applied change if something failed midway.
- **Fix:** Build a single commit with the Git Data API: create blobs, then one tree with a base tree, then one commit, then update the ref. File deletions go in the same tree with `sha: null`.
- **Rule:** One commit per meaningful change, with a message that says what it does.

## The web session expires, and sign-in codes expire fast

- **Mistake:** Relying on a saved GitHub web session from an earlier day, and sending a sign-in prompt while the owner was away.
- **Symptom:** Admin steps found the session signed out. The mobile approval prompt or device code expired before the owner saw it, so another round trip was needed.
- **Root cause:** Web sessions time out. GitHub Mobile prompts and emailed device codes are only valid for a few minutes.
- **Fix:** Check the signed-in state first. Trigger the sign-in only when the owner is active, tell them it expires in minutes, and have everything else ready so the session is used immediately.
- **Rule:** Check sign-in state before any admin step, and batch all admin work into the window right after a fresh sign-in.
