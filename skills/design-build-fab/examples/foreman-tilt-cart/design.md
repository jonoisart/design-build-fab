# Example: tilt cart for a Onefinity Foreman CNC

A rolling steel cart for a 48 x 48 in CNC router that cuts flat and tilts upright to park. This is the worked example behind `model.html`. Units are inches.

## Verdict

Build everything from one size: 2 x 2 x 11 ga (0.120 in) square tube, about 74 ft, which is four 20 ft or 24 ft sticks. Skip angle iron. At nearly the same weight per foot, closed square tube is roughly 90x stiffer in torsion, and a tilting top depends on torsional stiffness.

The cart is a 36 x 74 in base on casters with an A-frame post at each end, and a 60 x 60 in top that pivots on two 1 in pillow blocks. It cuts at 0°, leans at 80°, and parks at 90°. Parked, it needs about 18.5 sq ft of floor instead of the machine's roughly 70 x 75 in working envelope.

## Machine dimensions

| Dimension | Value | Source |
| --- | --- | --- |
| Cut area | 48 x 48 in | Onefinity |
| Feet, outside to outside | ~58-3/8 x ~60-1/16 in | [Owner measurement](https://forum.onefinitycnc.com/t/can-someone-measure-their-elite-foreman-feet-for-me/25724) |
| Full envelope incl. motors, wires, screen | 70 x 75 x 25 in | [Onefinity on its forum](https://forum.onefinitycnc.com/t/foreman-detailed-sizing/18788) |
| Fits on | a 5 x 5 ft sheet, ~1/32 in overhang | [Owner](https://forum.onefinitycnc.com/t/foreman-detailed-sizing/18788) |
| Foot bolts | 8 mm recommended over the supplied wood screws | [Forum](https://forum.onefinitycnc.com/t/can-someone-measure-their-elite-foreman-feet-for-me/25724) |

Measure before cutting steel: foot centers and pad size, X stepper overhang, cable and drag chain reach, gantry height.

## Manufacturer limits

Onefinity's wall-mount kit covers only the Woodworker and Journeyman, with a Makita router and the X axis vertical ([listing](https://www.matterhackers.com/store/l/onefinity-wall-mount-system/sk/MUZS0M04)). The Foreman is not offered for vertical cutting, and Onefinity says Elite machines are not supported on a wall ([forum](https://forum.onefinitycnc.com/t/wall-mounting-the-elite-series/17695)). So the cart cuts horizontal and only parks vertical, powered off.

## Material comparison

| Section | lb/ft | Bending I (in⁴) | Torsion J (in⁴) | Verdict |
| --- | --- | --- | --- | --- |
| 2x2x11 ga square | 3.06 | ~0.50 | ~0.80 | Use for everything |
| 2x2x14 ga square | 2.17 | ~0.39 | ~0.59 | Cheaper, easier to burn through, weaker at pivot ears |
| 2x3x11 ga rect | 3.89 | ~1.42 | ~1.48 | Overkill at a 60 in span |
| 2x2x3/16 angle | 2.43 | ~0.27 | ~0.008 | Cheapest per foot, racks badly |

I and J are hand calculations with sharp corners, so treat them as +/-10%.

## Design

- **Top (rotating)**: 60 x 60 in perimeter, three spines at x = 0 and ±17 in, 3/4 in Baltic birch sub-top, 3/4 in MDF wasteboard. Pivot ears are bolted on with three hole heights, so you can balance the loaded top.
- **Base**: 36 in end rails at ±36 in, 70 in long rails between them, one 26 in post per end braced into an A. Four 4 in total-lock casters, and four leveling feet that take the load off the casters while cutting.
- **Locks and props**: a pin through a post bracket into a lock disc on each axle, with holes at 0°, 80° and 90°. Props under the outer spines; the two on the side that drops are pull-pin removable.

| Item | Value |
| --- | --- |
| Pivot center above floor | 35 in |
| Wasteboard surface | ~37.5 in |
| Lowest point of top when parked | ~5 in |
| Parked height | ~69 in |
| Rotating mass | ~400 lb |

## What the model caught

The first layout put the posts at ±33 in. Sweeping the 3D model to 90° showed the low-side Y stepper motor swinging to about 7 in off the floor, right through the base end rails. Moving the posts to ±36 in fixed it. That cost 6 in of base length and longer stub axles, and still fits in four sticks.

## Cut list

| Part | Qty | Length |
| --- | --- | --- |
| Top front and back rails | 2 | 60 in |
| Top side rails | 2 | 56 in |
| Top spines | 3 | 56 in |
| Base long rails | 2 | 70 in |
| Base end rails | 2 | 36 in |
| Posts | 2 | 26 in |
| A-frame diagonals (cut to fit) | 4 | ~29 in |
| Props | 4 | 26 in |

Total about 884 in (73.7 ft, ~226 lb). Hardware: 3/8 in plate for ears, post tops and lock discs; 1 in cold-rolled round for stub axles; two UCP205-16 pillow blocks; 5/8 in lock pins; casters; leveling feet.

## Build sequence

1. Set the machine up on the floor and measure it before cutting anything.
2. Weld the top flat on a reference surface, alternating sides, then check that the diagonals match.
3. Weld the base and posts. Run one straight rod through both pillow blocks before the final welds.
4. Weld the stub axles to the ears on that same rod so they stay coaxial.
5. Hang the empty top, then set the lock holes and props.
6. Mount the machine, choose the ear height that balances the loaded top, then drill the 80° and 90° lock holes.
7. Leave a service hole in the sub-top under each foot, for motor wiring access.
