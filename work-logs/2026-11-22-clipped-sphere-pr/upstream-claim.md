Fixes #20780

A blind bore cut from the flat underside of a clipped sphere can remain sealed. The fork contains a test-only reproduction and a fix that makes the bore open at the correct radius.

Units: curve.curve_p6, curve.curve_p8, curve.ellipse_p1, curve.ellipse_p2, intersect.curve_class_p1, intersect.curve_class_p2, intersect.curve_class_p3, intersect.curve_class_p5, intersect.curve_class_p9, intersect.point_class, query.face_p2, topology.face_p3, topology.vertex, topology.proto_topology_p1, topology.proto_topology_p3, boolean.topology_intersector_p2, surface.plane_p1

In scope: distinguish nearby rims at their local tolerances during edge classification, endpoint snapping and vertex merging. Preserve the analytic planar trim for a circular bore.

Expected edits: the kernel’s curve and point classifiers, face and vertex topology and planar projection, plus the native Boolean regression and the recorded subtraction.

Evidence: the original axial ray stops at z = −6 mm in a two-shell body. The corrected ray reaches z = 0 mm in one shell. [Before-and-after geometry and kernel switch comparisons](https://github.com/shangaslammi/solidcraft/tree/50b195f027599a08a2571f4d5c5596289fadda34/work-logs/2026-11-22-clipped-sphere-pr)

Related PRs / dependencies: the [coplanar-face PR](https://github.com/tangency-labs/solidcraft/pull/13562) changes the edge-copy path of the same routine. The new separation checks apply to intersections of two surfaces.

Available follow-ups: the straight rectangular groove still disappears at 12.5 and 15 nm. [Groove and overhang tolerance tracker](https://github.com/tangency-labs/solidcraft/issues/20073)

Status / blockers / next step: the fork contains both commits and their validation. The change is ready for kernel review. [Submission branch](https://github.com/shangaslammi/solidcraft/tree/92bbf163485affb9a5cb0476fff7ae400b2063c8)

Changes a default: no
