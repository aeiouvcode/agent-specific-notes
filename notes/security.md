# Security

## A strict CSP broke the app's own downloads

- **Mistake:** Locking `connect-src` down to the model host without following its redirects.
- **Symptom:** Every model download failed with "Load failed, failed to fetch".
- **Root cause:** The model host redirects to a CDN origin the policy did not allow.
- **Fix:** Allow the exact redirect targets, and test the policy by actually downloading through it.
- **Rule:** After writing a CSP, exercise every network path the app has. A policy that is only reviewed, not run, will break something.

## Raw errors on screen read as malware

- **Mistake:** Letting stack traces and raw network errors reach the UI.
- **Symptom:** The owner said a raw error on his phone felt like he had downloaded malware.
- **Fix:** Catch errors and show a plain-language message with a next step.
- **Rule:** Error handling is part of the design and part of the security posture. Never surface raw errors.

## Standing checks for every cycle

Run these before every push:

- No secrets in the repo or its history (scan tracked files for key- and token-shaped strings)
- No unexpected outbound calls; the CSP matches what the app actually needs
- Remote scripts pinned with Subresource Integrity, or vendored
- No `innerHTML` sinks fed by untrusted input; sanitize any dynamic SVG or HTML
- Local data encrypted at rest where the app stores anything personal (AES-GCM with a PBKDF2- or Argon2-derived key, passphrase never stored)
- Nothing phones home: no analytics, no trackers

- **Rule:** Local-first by default. No backend unless the brief needs one, no secrets in any repo.
