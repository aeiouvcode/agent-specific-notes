# Engines and tooling

## Standing rule: use Godot when a build needs an engine to get closer to its reference

Owner directive, 2026-09-23 10:36, applies to the whole fleet:

> "Anything that requires a game engine for further improve to stand close to the ground truth, use the game engine godot"

- **Rule:** When a project cannot get closer to its reference (the "ground truth" the owner sent) without a game engine, build it in Godot. Do not reach for Unity, Unreal or another engine, and do not keep piling hand-rolled code onto a web renderer that has stopped closing the gap.
- **When it applies:** the remaining gaps are engine work: real physics, authored animation, lighting and optics the current renderer cannot reach, scene tooling, or performance that hand-written WebGL cannot hold on a phone.
- **When it does not:** apps, tools and builds already matching their reference in plain web tech. Moving those to an engine adds weight and gains nothing.
- **Precedent:** "Use godotengine for the fish gamr" (2026-09-22 09:09) moved KIN off hand-rolled web rendering. [kestrel9-godot](https://github.com/aeiouvcode/kestrel9-godot) is an existing Godot 4 web build on this account.

## Polishing a renderer past its ceiling

- **Mistake:** Iterating on fake physics and shader tricks in a hand-rolled web renderer long after it stopped closing the gap to the reference.
- **Symptom:** "Physics not there for fluid sim", "this is nothing like the video" (Stillwater, 2026-09-21). Milestones kept shipping, but the side-by-side barely moved.
- **Root cause:** The gap was engine-level (simulation, lighting, animation), and each milestone treated it as a tuning problem.
- **Fix:** When two review cycles in a row show the same engine-level gap, stop tuning. Propose the Godot move and log it in the project's handoff.
- **Rule:** Name the ceiling early. If the reference needs an engine, move to Godot. Do not fake the effect.

## Before switching a project to Godot

- **Rule:** Keep the permanent home. The Godot web export ships to the same GitHub Pages URL, or the README links the new one.
- **Rule:** Probe the web export on a phone-width viewport with a minimal scene before porting everything. Load time, touch input and frame rate decide whether the port is viable. Record what the probe showed ([working-protocol.md](working-protocol.md#guessing-how-an-unstable-api-behaves)).
- **Rule:** The reference stays the acceptance bar. An engine switch that does not visibly close the side-by-side gap is not done ([design-rules.md](design-rules.md#references-are-the-spec)).
