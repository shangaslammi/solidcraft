# Opening a bore at a clipped sphere’s rim

The 10 mm sphere has an 8 mm rim at z = −6 mm. A coaxial cutter of radius 8 + d
reaches z = 0. For positive d its wall meets the sphere at z = −√(100 − (8 + d)²).

| Bore offset d (mm) | Previous result | Correct lower edge z (mm) |
| --- | --- | --- |
| +0.0000125 | The classifier put the sphere–cylinder intersection on the cap rim. Conflicting edges caused the Boolean to refuse the cut. | −5.999983333297 |
| +0.0000150 | Four cap arcs survived alongside the true intersection. The body failed three validity checks and record export. | −5.999979999948 |

Both radii lie between the 0.00001 mm coincidence tolerance and the 0.00002 mm
intersection-search distance. The kernel had already found the correct intersection.
Its height above the cap is 0.000016667 mm in the first case and just over 0.000020000 mm
in the second. The wider search let the classifier join distinct rims at a seam.

The classifier now checks separation over the whole rim before assigning a shared edge,
snapping a crossing to a seam endpoint, or merging vertices. It uses the native curves
or either surface defining their intersection. This preserves real crossings in an
oblique drill and an eccentric notch. At a shallower clip, z = −8 mm, the cylinder
proves the rims separate even when their height difference is only 0.000009375 mm.

Rotating the cutter seam also exposed a planar trim error. At d = −0.00002 mm and
0.37 radians, the 3D circles were correct but the fitted inner trim gave an annular
area of 0.001142361432 mm². The plane now preserves the exact rational trim when the
whole ellipse fits inside its parameter bounds. The measured area is 0.00100530839245 mm²,
matching the circles.

On upstream `eea94c41b`, all 128 offset and seam checks and 19 geometry variations
passed, including changed radii, clip depths, placements and tenfold tolerances. For both
requested offsets the bore-axis ray hit the ceiling at z = 0 and the lower edge was within
5×10⁻¹⁵ mm of the analytic height. All 25 targeted kernel and Boolean tests and all
37,909 golden cases in the 16 affected units passed. Both workspace Clippy checks
and the kernel’s WebAssembly build check passed. [Verified code](https://github.com/shangaslammi/solidcraft/commit/4fe4f7ac9)

Merging the two upstream UI commits through `c95c2bef4` kept the fork’s verified
`solidcore` Git tree at `bebb233b9`.

The straight rectangular groove still disappears at depths of 0.0000125 and 0.000015 mm.
Its line-edge classification is tracked in [SolidCraft issue #20073](https://github.com/tangency-labs/solidcraft/issues/20073).
