# Design rules

## One template skin across every app

- **Mistake:** Many apps shipped with the same dark-terminal look: near-black background, green accent, boxes inside boxes.
- **Symptom:** The whole portfolio was rejected as looking templated and machine-made.
- **Root cause:** Reusing a default visual system instead of giving each project its own art direction.
- **Fix:** A redesign wave across the portfolio. Each app got its own palette, type and composition, drawn from its subject.
- **Rule:** The dark-terminal / green-accent / nested-card skin is banned. Every project gets its own art direction.

## Restraint over decoration

- **Rule:** Minimal and quiet by default. Spend visual weight only on the parts of the page that matter.

## Color must sit with the ground

- **Mistake:** A cobalt accent on a warm paper background.
- **Symptom:** Rejected: the blue did not fit the background.
- **Fix:** Replaced with a warm mineral rust.
- **Rule:** Judge an accent against its background, not on its own.

## References are the spec

- **Rule:** When the owner sends a reference image or video, it is the target, not a mood board. Match its camera, composition, motion and lighting, then compare side by side.

## Component libraries are pattern sources

- **Mistake risk:** Pasting showcase components from UI libraries.
- **Root cause:** It recreates the template collage the first rule bans.
- **Rule:** Borrow interaction quality (pressed states, easing, spacing) and reimplement it natively in the project's own style.

## Depth and light are requirements

- **Rule:** Where the subject is physical (water, light, 3D worlds), depth, lighting and optics are part of the brief, not polish for later.
- **Rule:** If reaching the reference needs a game engine, use Godot. See [engines-and-tooling.md](engines-and-tooling.md).

## Mobile first means checked at 390px

- **Rule:** Touch controls, HUD layout and text sizes are verified on a 390px-wide viewport before a build counts as done.
