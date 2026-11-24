# Partial-cylinder trim certificates

The upper circular edges of `gen0329` and `gen0533` fit their planar caps, although a control point of each curve crosses the cap's UV bounds. The exact projection keeps each edge and its endpoints within the tolerance already set by stitching. Only three of the 281 raw values change in each case, at positions 12, 28 and 173. [Merge-queue review](https://github.com/tangency-labs/solidcraft/pull/20844#issuecomment-7140802301)

| Case | Previous tolerance (mm) | New tolerance (mm) | Cap gap bound (mm) | Wall gap bound (mm) | Canonical row digest |
| --- | ---: | ---: | ---: | ---: | --- |
| `gen0329` | 1.5721457101882903e-5 | 1.5686721568173903e-5 | ≤ 2.434e-8 | ≤ 4.706e-8 | `7951f9c3f96cf363` |
| `gen0533` | 1.849262309506995e-5 | 1.8468663337512777e-5 | ≤ 1.847e-8 | ≤ 1.847e-8 | `93329193f77386ba` |

Both tests that failed in the merge queue now pass using Ubuntu 24.04’s math runtime. The fillet case `stubs4-degenerate-test5-e5-r0.5` has identical raw output on main and the PR on that runtime. Restoring the historical primitive values reproduces the unit digest `9ee3ca6ac55fd5b5`. [Certificate commit](https://github.com/shangaslammi/solidcraft/commit/35b3290f406268cca2245ff9c75d5184f5afd7ce)
