# Architecture and proposed decisions

**Draft · 2026-11-03. Tests NOT RUN.** Contract: [SPEC](SPEC.md). Stages and tests: [implementation](IMPLEMENTATION_PLAN.md), [verification](VERIFICATION_PLAN.md).

## Data flow and topology

`FamilyContract + Geometry + MeshingOptions → validate → landmarks → block graph → spacing → generate/smooth → global quality → MeshResult → export`. Optimize by feeding an update through the same pipeline; never reuse a failed artifact as a valid mesh.

The candidate v1 topology is a **hypothesis**: a ring of four structured quadrilateral blocks between one blade and a rectangular passage. Four distinct ordered blade anchors split the contour into upstream cap, upper side, downstream cap and lower side; leading/trailing edge landmarks lie on the caps. Their corresponding outer arcs are inlet, upper periodic, outlet and lower periodic. Four noncrossing radial seams join anchors to rectangle corners. Neighboring blocks share seam nodes; upper and lower outer arcs have identical x-distributions and pair by translation `(0, pitch)`, with opposite boundary traversal. Use compatible interval counts on opposite sides of each block.

P0 must test whether deterministic anchor placement remains unique and ordered across the bounded family, seams avoid the blade and each other, periodic sides match, and blunt or sharp trailing-edge treatments remain valid. Define accepted feature types and forbidden contour/landmark bifurcations; include difficult endpoints and nearby parameter changes in exploratory cases. If evidence does not support the O-grid, select another explicitly described single topology family and revise the contract, graph, tests and decision before P1; do not imply a failed hypothesis binds the product. At runtime reject features or branch changes outside the selected contract rather than silently switching topology.

All input coordinates and length parameters are explicitly meters in a right-handed Cartesian x-streamwise/y-pitchwise frame; pitch is positive. Dimensionless settings are tagged separately. Require finite values, a closed non-self-intersecting contour, positive area/chord and pitch, nonintersecting periodic images, positive first height, integer positive layers, feasible growth and admissible bounds. Normalize internally only with a recorded positive reference length, restore SI at export. Define tolerance as a contract-relative length, not a guessed absolute unit. Boundary IDs are `blade`, `inlet`, `outlet`, `periodic_lower`, `periodic_upper`; stable semantic names are separate from node IDs.

## Records and state

- `FamilyContract`: schema/version, geometry parameter names and ranges, representation, domain, landmarks, feature/branch constraints, tolerances, selected topology and corpus IDs. Acceptance run records separately bind a test-contract hash; exploratory runs have no acceptance threshold requirement.
- `Geometry`: ordered points/curve parameters, coordinate frame, units, pitch, stable feature IDs and contract hash.
- `MeshingOptions`: spacing `(first_height_m, layers, growth)`, node counts, quality floors, smoothing/repair and resource budgets, seed, algorithm version.
- `BlockGraph`: ordered blocks, node counts, shared seams, boundary IDs and periodic transform plus node correspondence.
- `Mesh`: SI coordinates, oriented quad connectivity, boundary edges/IDs and metadata; export sidecar carries periodic pairing, units and frame because a mesh file alone may not.
- `MeshResult`: status, optional mesh, diagnostic codes/locations, actual spacing, minimum signed Jacobian and other metrics, repair history, provenance/cache hashes, timing and peak-memory measurements, sensitivity status.

Statuses: `OK`, `INVALID_INPUT`, `OUT_OF_FAMILY`, `TOPOLOGY_UNSUPPORTED`, `SPACING_INFEASIBLE`, `COLLISION`, `INVALID_CELL`, `BUDGET_EXCEEDED`, `EXPORT_ERROR`. Only `OK` contains an exportable mesh. Sensitivity status is separately `NOT_PROVIDED`, `SMOOTH_LOCAL_UNVERIFIED`, or `INVALIDATED`; v1 returns `NOT_PROVIDED` unless a later validated implementation exists. Diagnostic meshes, if emitted, must be explicitly marked non-solver-ready. A failure must not overwrite a previously accepted mesh.

## API and implementation choices (proposed, not existing)

Python library first: `validate(contract, geometry) -> diagnostics`, `generate(contract, geometry, options) -> MeshResult`, `update(previous, geometry, options) -> MeshResult`, `export_su2(result, path) -> report`. Pure-Python orchestration and array-based numerical kernels enable transparent iteration and easy optimization integration. Prefer a compiled kernel only after profiles show the approved resource budget cannot be met. Alternatives are C++/Rust core with Python bindings (performance and ABI costs) or a Gmsh/pyHyp adapter (less original code, dependency and topology constraints). P0 determines reuse; do not build a new mesher merely because this proposal exists.

Deform only if topology/feature IDs, counts and options remain compatible; propagate boundary motion with a deterministic scheme, rerun collision/Jacobian/global checks, and fall back to full remesh only within explicit policy and budget. All caches are content-addressed by canonical geometry, frame/units, contract, topology, options, seed, library/dependency versions and relevant algorithm settings. Changes invalidate descendants; no floating-point hashing of unstable serialization. Same pinned platform and single-thread mode target bitwise repeatability; cross-platform comparisons use preregistered tolerances. Determinism and resource limits are measured, not presumed.
