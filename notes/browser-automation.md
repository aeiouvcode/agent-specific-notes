# Browser automation

## Background and headless tabs throttle requestAnimationFrame

- **Mistake:** Measuring game or animation behavior in an automated browser tab and trusting the numbers.
- **Symptom:** Frame loops ran slowly or not at all, timers drifted, and hooks placed on the page's animation frame ran after the frame had already rendered. That made per-frame measurements misleading.
- **Root cause:** Browsers throttle `requestAnimationFrame` in tabs that are hidden, unfocused or headless. Page-level rAF hooks also run in an order you do not control relative to the renderer.
- **Fix:** For numeric checks, compute directly from scene state (for example, clone the camera and project points yourself) instead of hooking the render loop. For visual checks, take real screenshots of the live page.
- **Rule:** Do not treat frame rate or per-frame timing from an automated tab as ground truth. Measure state, and check visuals with actual screenshots.

## A login in one session is not visible to parallel sessions until it is saved

- **Mistake:** Starting a second browser session right after a sign-in succeeded in another one, and expecting to be signed in.
- **Symptom:** The new session was signed out, even though the account had just been signed in elsewhere.
- **Root cause:** When several jobs share one saved browser profile, new cookies are only written back when the session that captured them closes.
- **Fix:** Close the session that did the sign-in, then open the next one.
- **Rule:** Sign in, close that session so the profile saves, then start dependent work. Do not start parallel browser work against an account that is mid-login.

## Shared browser capacity runs out

- **Mistake:** Scheduling deploys and phone-width QA assuming browser time was unlimited.
- **Symptom:** Work stalled for hours after the daily browser allowance ran out.
- **Root cause:** Browser time is a shared, capped resource.
- **Fix:** Ship to a preview surface first and batch the browser-dependent steps (Pages push, mobile QA) into the next window.
- **Rule:** Batch browser work. Do API-level work (pushes, reads) without a browser wherever possible.

## Tag inputs in web forms often commit the suggestion, not what you typed

- **Mistake:** Typing a value into an autocomplete tag field and pressing Enter.
- **Symptom:** A different, suggested value was saved, or typed text merged with a previous token.
- **Root cause:** Enter selects the highlighted suggestion. A delimiter character can also stay in the input and prefix the next token.
- **Fix:** Commit each tag with its delimiter, clear any leftover character, and read the resulting tokens back before saving.
- **Rule:** After filling any autocomplete or token field, read the final value back before submitting.
