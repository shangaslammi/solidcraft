# A bore starting at a clipped sphere’s rim

Clipping a 10 mm-radius sphere at z = −6 and 7 mm leaves a bottom disc of radius 8 mm.
On upstream main `22a3aa1df`, subtracting a coaxial cylinder from that disc up to z = 0
left a sealed cavity when the cylinder’s radius was 0.00001 mm inside the rim. The disc and
the tool cap both covered the mouth. A ray from below hit the skin at z = −6 mm, even though
the volume matched the analytic result and every body check passed.

The face intersections found the shared rim. When the boolean rebuilt the overlapping edges,
it checked them at 0.000005 mm, half the tolerance of either edge, and discarded the rim.
Commit `2e8401099` uses both edges’ zone tolerances and the kernel’s existing rounding
allowance for this comparison.

| Bore radius minus rim radius | Before | After |
| --- | --- | --- |
| −0.000005 mm | Only a quarter of the rim survived. The cut returned the unbored volume. | Open bore, one shell, volume 2292.3169475 mm³. |
| −0.00001 mm | A complete disc covered the bore. | Four faces in one shell. The ray reaches the ceiling at z = 0. Volume 2292.3184555 mm³. |
| −0.0001 mm | A narrow annulus surrounds the opening. | The annulus survives, with area 0.005026517 mm². |

The regression checks the first face reached by a ray up the axis and by another just inside
the rim. It also checks shell count, volume and full body validity. It fails on the upstream
parent and passes on the fix. Rotating the cylinder seam by 90° also gives an open bore.
Six related boolean regressions passed. All 3,013 cases for `topology.proto_topology_p3`
and 3,138 cases for `curve.curve_p6` matched their recorded results.

Across the 24 offsets in the original report, 22 give a valid single shell with an open bore.
The two cases exactly 0.00002 mm inside and outside the rim still fail `CheckLevel::All`.
The outside case also fails record conversion. Running the seven critical offsets with all
opt-in fixes enabled gives the same two exceptions.
