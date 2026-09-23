# Deploys and hosting

## Anonymous hosts expire and take finished builds with them

- **Mistake:** Early builds were shared as anonymous drop links on temporary paste and static-drop hosts.
- **Symptom:** A day later the link was dead. Two finished builds (the first O Empire prototype and the first ISSEN) were lost and had to be rebuilt from scratch.
- **Root cause:** Anonymous deploys on those hosts expire after roughly 24 hours, and no copy of the source was kept anywhere permanent.
- **Fix:** Every project now lives in its own repository on this account with GitHub Pages as the permanent URL.
- **Rule:** Never hand over a link that can expire. The source goes into a repo first, and the link given out is the Pages URL.

## A deploy is not done until the live URL serves the new bytes

- **Mistake:** Reporting a deploy as done right after the push succeeded.
- **Symptom:** The owner opened the link and saw the previous version, or a 404 while Pages was still building.
- **Root cause:** Pages builds are asynchronous and cached. A successful push only means the commit landed.
- **Fix:** After pushing, poll the live URL until a hash of the served file matches the local file, then load it in a browser.
- **Rule:** "Live" means the served file hash matches what was tested and the page boots. Nothing less.

## Temporary previews have their own sandbox limits

- **Mistake:** Treating an in-app preview link as equivalent to the Pages deploy.
- **Symptom:** Audio would not play, saves did not persist, and apps that load models from external hosts failed to start.
- **Root cause:** Sandboxed preview surfaces block inline audio, localStorage and external scripts.
- **Fix:** Use the preview for fast review only. Ship anything that needs audio, storage or remote assets to Pages.
- **Rule:** Check what the target surface allows before choosing it. The permanent home is always the repo and its Pages site.

## Deleting a file without checking references breaks the live site

- **Mistake (avoided):** Cleaning up "unused" build output in a repo.
- **Root cause risk:** Pages serves whatever `index.html` references. A file that looks stale may still be loaded.
- **Fix:** Before deleting, search `index.html` and every script for the file name. After the cleanup commit, reload the live site.
- **Rule:** Never move or rename deploy-critical files (`index.html`, engine exports, chunked bundles). Delete only what nothing references, then verify live.
