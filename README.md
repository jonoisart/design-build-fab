# design-build-fab

An open-source agent skill for designing things you'll actually build: carts, machine stands, tables, frames, jigs, fixtures and furniture.

It works through each build the same way:

1. Research the real dimensions and cite where each one came from.
2. Pick material by stiffness per dollar.
3. Check loads and stability.
4. Write a design doc with a cut list, an order and a build sequence.
5. Build an interactive 3D model and sweep every moving part through its range to catch collisions before you cut steel.

## Contents

| Path | What it is |
| --- | --- |
| `skills/design-build-fab/SKILL.md` | The skill: workflow, model architecture, quality bar |
| `skills/design-build-fab/SHOP.example.md` | Template for your own shop profile (copy to `SHOP.md`, which is gitignored) |
| `skills/design-build-fab/examples/foreman-tilt-cart/` | Worked example: a tilt cart for a 48 x 48 in CNC router, with its design notes and interactive model |

## Install

- **Claude Code**: copy `skills/design-build-fab` into `~/.claude/skills/` (all projects) or `.claude/skills/` (one project).
- **Claude apps**: zip the `skills/design-build-fab` folder and upload it as a skill.
- **Other agents**: point the agent at `SKILL.md`; it's plain Markdown.

Then copy `SHOP.example.md` to `SHOP.md` and fill in your region, units, suppliers and tools.

## Try the example

Open `skills/design-build-fab/examples/foreman-tilt-cart/model.html` in a browser. Drag to orbit, then tilt the top from cutting to parked and watch the clearance readouts.

## Safety

This skill produces design aids, not stamped engineering. Anything that carries people, hangs overhead, or could hurt someone if it fails needs review by a licensed engineer.

## Roadmap

- CAD export (OBJ/STEP) from the parts list
- Per-part cut and weld drawings
- Parametric sliders for key dimensions
- A sibling skill that scales the method up to architectural projects

## Contributing

Issues and pull requests are welcome, especially new worked examples. Keep personal details out of commits; they belong in your local `SHOP.md`.

## License

MIT
