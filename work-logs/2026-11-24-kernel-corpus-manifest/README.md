# Clipped-sphere corpus replay after merging main

The corpus test on main now counts the case files itself. The clipped-sphere subtraction can be replayed from its two saved operands, so the PR contributes only the case and operand files to the corpus. Both files have the same Git blob IDs as before the merge. [Upstream review](https://github.com/tangency-labs/solidcraft/pull/20844#issuecomment-7103157713)

The vector norm and main’s new acute-angle tangent-edge bound now share the same interval-square function. The ellipse-line tangency regression from main passes an unrestricted endpoint mask so it still searches both ends of the curve. [Merge commit](https://github.com/shangaslammi/solidcraft/commit/f6dc8825bb43309a4c3a8c88d7bda12acbb2ecb6)

The corpus validator, clipped-sphere replay, bore regression, rounded-outset check and both tangency tests passed. The replay reported zero relative volume deviation. All 45,692 golden cases across the 19 affected units matched their committed outputs. Both workspaces passed Clippy and the kernel passed the WebAssembly build check. [Upstream PR](https://github.com/tangency-labs/solidcraft/pull/20844)

## Compatibility with typed topology errors

Main subsequently added typed errors to the same import list in proto-topology. The shared-edge search now names `crate::error::ignored` at its only call site in that module. Git merges the PR cleanly with upstream `ad3164473`. On the combined tree the bore replay passed with zero relative volume deviation, and all 4,935 golden cases across the two affected proto-topology units matched their committed outputs. [Import change](https://github.com/shangaslammi/solidcraft/commit/f1b0521706f41a9c8abbb738b88e38719d12ac9b) · [Upstream main](https://github.com/tangency-labs/solidcraft/commit/ad316447348446d499957cecf84693a59d7cb4cb)
