# A bore starting at a clipped sphere’s rim

A 10 mm-radius sphere clipped at z = −6 and 7 mm has a bottom disc of radius 8 mm.
A coaxial cylinder cuts from that disc up to z = 0. On upstream `22a3aa1df`, when
its radius was 0.00001 mm inside the rim, the volume and every body check passed,
yet a ray up the bore hit a zero-thickness skin at z = −6 mm.

| Bore radius minus rim radius | Before | After |
| --- | --- | --- |
| −0.000005 mm | Only a quarter of the shared rim survived. The cut returned the unbored volume. | Open bore, one shell, volume 2292.3169475 mm³. |
| −0.00001 mm | A complete disc and the tool’s cap sealed the bore. | One open bore with four faces. A ray up its axis reaches the ceiling at z = 0. |
| −0.00002 mm | The annulus shared a vertex between its two rims and failed the full body check. Its measured area was 0.000845309 mm². | The two rims have distinct vertices. The bottom face measures 0.001005308 mm², matching π(8² − 7.99998²). |
| +0.00002 mm | The result was nonmanifold and could not be written to a B-rep record. | The bore wall meets the sphere at z = −5.999973333 mm. The bottom disc is gone. |
| −0.0001 mm | A wider annulus surrounded the opening. | The annulus still measures 0.005026517 mm². |

Commit `2e8401099` uses the native edge tolerances and part-scale rounding when it
rebuilds a shared rim. At twice the zone tolerance, a separate fault in the intersection
search gave different answers around two concentric circles. Commit `8894c6dc2` uses the
semi-axis bounds to establish separation over both arcs and at their vertices when the
two search bands meet at their outer limit. This preserves the valid open bore at
+0.0000101 mm.

The regression checks the first surface hit from below, shell count, analytic volume,
record conversion and full body validity. It also measures the inner annulus and the
lowest vertex on the outer cut. All ten targeted boolean tests passed against upstream
`df0859994`. Both 0.00002 mm cases also passed with the cylinder seam rotated 90°.

All 24 offsets from the original report produced one valid shell with an open bore,
a valid record and the expected volume, both with the default kernel and with all
optional fixes enabled.

Two additional positive offsets still reproduce failures present before this change.
At +0.0000125 mm the boolean refuses the cut. At +0.000015 mm it returns a nonmanifold
body. The disagreement between tolerances inside this band is tracked for other
geometries in [SolidCraft issue #20073](https://github.com/tangency-labs/solidcraft/issues/20073).
