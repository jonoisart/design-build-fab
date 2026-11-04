---
name: design-build-fab
description: Design a physical build (cart, table, stand, frame, jig, fixture, furniture) end to end: real dims, material choice, design doc with cut list, and an interactive 3D clearance model.
---

# Design build fab

A method for designing things you will actually fabricate. The output is a build you can order material for and assemble: researched real dimensions, a defensible material choice, a living design doc with a cut list, and an interactive 3D model that proves every moving part clears.

Use it for carts, machine stands, tables, frames, jigs, fixtures, enclosures and furniture. Scale effort to the build: a simple bracket may only need steps 2, 4 and 6.

## Shop profile

If a `SHOP.md` file sits next to this skill, read it first and use it for defaults: region, units, suppliers and stock lengths, tools, space constraints, voice. `SHOP.example.md` is the template; `SHOP.md` is gitignored so personal details never land in a public repo. With no profile, use what the user has told you elsewhere, or ask once for units, region and how they join material (weld, bolt, screw).

## Workflow

1. **Intake.** Pin down what the build carries or houses, its operating states (fixed, rolling, tilting, folding, stowed), the space it must fit or stow in, units, region, joining method, and budget. Ask only for what changes the design; list the rest as open questions.
2. **Research real dimensions.** Search manufacturer manuals, spec sheets and owner forums for anything the build carries or fits. Fetch the pages, cite them, and record each number with its source. Where official data is missing or ambiguous (which axis is which, model generations, cables and connectors not counted), say so and add a measure-before-cutting checklist.
3. **Check the manufacturer's limits.** Find what the maker does not support (orientation, mounting, loads, warranty terms) and state it plainly. Design around it rather than burying it.
4. **Choose material by stiffness per unit cost.** Material cost tracks weight, so compare candidate sections in one table: weight per length, bending I, torsion J, joining method, verdict. Closed tube beats open angle in torsion by roughly 90x at similar weight, so anything that tilts, racks or cantilevers wants closed sections. Consider aluminum extrusion or wood when the user's tools favor them. Prefer one size for the whole build: one stock length, fewer orphan drops, one welder or saw setup. Mark hand calculations as +/-10%.
5. **Check loads and stability.** Estimate total mass and center of mass. Check caster or foot ratings with at least a 1.5x margin, tipping (base half-width vs center-of-mass height, and push-over at the worst handle position), the torque needed to move any mechanism, and deflection of the longest span (PL³/48EI for a center load, 5wL⁴/384EI for a uniform one). Anything that carries people, hangs overhead, or could injure on failure needs review by a licensed engineer; say so.
6. **Write the design doc** (a shareable doc artifact where available, otherwise a Markdown file), one section at a time:
   - Verdict: material and concept in two short paragraphs
   - Dimensions: sourced table plus measure-before-cutting checklist
   - Caveats: manufacturer limits and safety notes
   - Material comparison table
   - Design: geometry by assembly, heights and clearances table, operating procedure
   - Cut list with stock nesting and kerf, a supplier order line, hardware table, budget marked approximate unless quoted
   - Build sequence: weld or assemble flat on a reference surface, align bearings with a straight rod before final welds, test-fit order, service access
   - Open questions
7. **Build the interactive 3D model** as a standalone page (published artifact or local HTML file). Inline chat widgets may fail to render in some mobile apps, so prefer a standalone page. Then use it as a design check, not an illustration: sweep every moving part through its full range and look for collisions and floor or ceiling clearance. Feed any clash back into the doc right away and tell the user what the model caught.
8. **Close** with a line or two: what was made, what the model caught, and the next real step (measure the delivered item, export to CAD, get a supplier quote).

## 3D model architecture

Working reference: `examples/foreman-tilt-cart/model.html`. Copy it and swap the parts list rather than starting over.

- **Data-driven parts list** in real units: `box(group,[sx,sy,sz],[x,y,z],mat,tag)`, `cyl(group,r,len,axis,[x,y,z],mat,tag)`, `strut(group,[a],[b],width,mat,tag)` for diagonals. Axes: x across, y up, z along the main pivot or length. One color map by material role (tube, plate, bearing, wood, sheet goods, aluminum, black hardware, removable/warning red).
- **Groups for mechanisms**: a static base, with rotating or sliding sub-assemblies nested (e.g. top > gantry > carriage). One `toWorld(group, point)` function applies the same transforms for both renderers, the labels and the metrics.
- **Renderer 1**: three.js r128 UMD from cdnjs (`https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js`), MeshStandardMaterial, EdgesGeometry outlines on boxes, a hemisphere light plus two directional lights, a floor grid at 1 ft or 300 mm squares, and the floor footprint outlined in the accent color.
- **Renderer 2 (fallback)**: canvas 2D painter's algorithm. Convert every part to 8 corners, transform, project, sort faces by depth, Lambert shade. Switch to it on a fresh canvas if three.js is missing or WebGL fails, and show a small "Simplified renderer" badge.
- **Controls**: a slider plus preset buttons for mechanism states (eased tween, respects reduced motion), view presets (three-quarter, along axis, side), pointer orbit, two-finger pinch zoom, wheel zoom, labels toggle. Put `touch-action:none` on the 3D stage only.
- **Live readouts computed from the geometry**, never typed in: lowest point, overall height, floor footprint and area, a state chip, and a procedure checklist that changes with state (e.g. pull props before tilting). Hide parts that are removed in a given state.
- **Labels**: HTML chips projected from 3D anchor points, hidden when off-stage.
- Render on demand (dirty flag), use a ResizeObserver, use theme tokens for light and dark, lay out mobile-first, and syntax-check the script (`node --check`) before publishing.

## Quality bar

- Every number is sourced, measured, computed, or labeled as an estimate.
- The model and the doc agree; when one changes, update the other in the same pass.
- Treat the first design as a hypothesis the model tries to break.
- Keep personal details (names, addresses, suppliers tied to a location) in `SHOP.md` or the user's private notes, never in shared outputs unless the user asks.

## Roadmap

Planned: CAD export (OBJ/STEP) from the parts list, per-part cut and weld drawings, parametric sliders for key dimensions, and a sibling skill that scales the method to architectural projects (buildings, structures, site work).
