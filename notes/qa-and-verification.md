# QA and verification

## Shipping without looking at the live build

- **Mistake:** Reporting a build as done based on code, DOM state or a successful export, without looking at it.
- **Symptom:** The owner found broken touch controls, overlapping HUDs, blank canvases and clipped text that a single screenshot would have shown.
- **Root cause:** Visual correctness can only be checked visually.
- **Fix:** Capture real frames of the deployed page at desktop width and at 390px phone width, inspect them, and include them in the report.
- **Rule:** No frame, no ship. Every delivery includes at least one screenshot of the live URL, and mobile builds are checked at 390px.

## Grading your own work too kindly

- **Mistake:** Calling a build a pass because it runs.
- **Symptom:** The owner compared it side by side with the reference and found it far off.
- **Fix:** A self-critique loop: compare against the actual reference, grade honestly (PASS / PARTIAL / FAIL), name the weakest element, fix it, repeat.
- **Rule:** Grade against the reference, not against the previous build. State what is still missing.

## Fake physics gets caught

- **Mistake:** Animated noise standing in for water, and a flat tilemap standing in for a 3D town.
- **Symptom:** Rejected on sight: it was not a simulation.
- **Root cause:** Choosing the look of a system over the system.
- **Fix:** A real 128x128 damped heightfield for water, true 3D geometry for the town builder.
- **Rule:** If the brief names a physical effect, simulate it. Say plainly where the simulation stops.

## Mock providers presented as intelligence

- **Mistake:** Shipping agent apps whose "AI" was a scripted or deterministic stand-in, without making that obvious.
- **Symptom:** The app looked smart in a demo and fell apart on real input, which undermined trust in every other claim.
- **Root cause:** A mock provider was kept as the default path instead of a clearly labelled fallback.
- **Fix:** Wire a real model provider (bring your own key, with free routes listed first), label any offline fallback on screen, and add honest-boundary copy to demonstrators that do not use a model.
- **Rule:** Never let a mock look like a model. If it is deterministic, the UI says so.

## Figures must come from the real run

- **Rule:** Numbers, diagrams and benchmarks in a report come from the actual build or simulation state, never from an illustration of what they would probably be.
