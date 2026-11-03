# Implementation plan

**Draft · 2026-11-03. Tests NOT RUN.** No task started. Requirement mapping: [SPEC](SPEC.md); acceptance tests: [verification](VERIFICATION_PLAN.md). Each task's verification is its same-numbered `V` test; DoD includes recorded result and review, not just code completion. T14 is optional and gates only experimental application claims.

## Tasks

| Task | Depends | Input → output | Verification and definition of done |
|---|---|---|---|
| T01 | none | Stakeholder needs → bounded family, protected corpus split and staged acceptance-contract process | V01: exploration labeled; applicable artifacts signed and immutable before acceptance; missing fields block. |
| T02 | T01 | Family, exploratory cases and rights → topology/reuse decision for pyHyp, Turbomesh, Gmsh, solver meshers, and new build | V02: record comparable exploratory evidence and license review; select one feasible topology, or stop/revise. |
| T03 | T02 | Family and geometry → validator/feature diagnostics | V03: valid plus malformed cases, units and image intersections classified. |
| T04 | T03 | Features and selected topology → deterministic block graph | V04: graph, shared seams and periodic map tested on family samples; unsupported cases fail. |
| T05 | T04 | Graph/mesh fixture → SU2 export and sidecar | V05: independent import preserves all cells, markers and transform; bad input rejected. |
| T06 | T04 | Valid geometry and spacing options → layer distribution | V06: first height, count, growth and infeasible inputs verified. |
| T07 | T06 | Generated layers and periodic images → collision diagnostics | V07: deliberate collisions and near misses classified; no valid output on collision. |
| T08 | T07 | Candidate quad mesh → global quality report | V08: inverted, folded, overlapping and missing-boundary fixtures rejected. |
| T09 | T08 | Invalid candidates and limits → bounded smoothing/repair | V09: constraints honored, every candidate rechecked, exhaustion fails closed. |
| T10 | T09, T05 | Previous result and new geometry → deform-or-remesh update | V10: path, repeatability, validation and resource budget recorded; failure cannot masquerade as success. |
| T11 | T10 | Pipeline dependencies → versioned cache/invalidation | V11: mutate each key component; no stale hits and cold/warm results agree. |
| T12 | T10 | Update behavior → sensitivity status contract | V12: branch/topology changes invalidate claims; no unsupported derivatives returned. |
| T13 | T11, T12 | Frozen cases, thresholds, pinned solver → refinement and baseline report | V13: all cases counted, convergence and QoI criteria applied; failures retained. |
| T14 | T13 | Optional rights-cleared independent measurements → experimentally assessed application-case package | V14: uncertainties, model discrepancy, exclusions, permissions and claim boundaries documented; no unsupported claim. |
| T15 | T13 | Reviewed code, distribution rights and numerical evidence → standalone library release candidate | V15: external clean-room reproduction, governance and license review recorded; T14 not required. |

## Actionable steps

- **T01:** Define family, provisional resource limits and training/exploratory fixtures. Seal held-out cases under an independent custodian; define run labeling and version history. Before each acceptance, approve the applicable corpus, solver, limits and contract hash; exercise rejection of missing approvals.
- **T02:** Compare candidate tools on recorded exploratory cases and inspect licenses. Spike anchor stability, seam feasibility, periodic pairing and branch constraints without held-out access. Record evidence and select one topology/reuse path, or revise the family and repeat.
- **T03:** Define geometry/unit schemas and stable feature identifiers. Implement finite, dimensional, closure, intersection, periodic-image and bounds checks. Add localized positive and negative fixtures and review diagnostics.
- **T04:** Encode the selected topology's features, block adjacency and interval compatibility. Generate seams and periodic correspondences deterministically. Test invariants and reject unsupported features or branch changes.
- **T05:** Serialize true 2D nodes, quads and named edges to SU2 plus a units/periodic sidecar. Independently parse and compare coordinates, orientation, markers and pairings. Reject invalid results or incomplete metadata.
- **T06:** Define first height as wall-to-first-node normal distance and compute the requested layer sequence. Check total thickness and parameter feasibility before generation. Verify actual heights and growth, with explicit infeasibility diagnostics.
- **T07:** Build collision checks for wall, layers, seams and periodic images. Exercise intersecting, touching and separated fixtures using contract tolerances. Prevent valid export on collision and report locations.
- **T08:** Compute signed bilinear Jacobians at all cell corners and quality metrics. Independently check cell overlap, boundary coverage and connectivity. Reject inverted, folded, degenerate or nonconformal cases.
- **T09:** Implement deterministic smoothing and bounded repair with protected boundaries. Enforce displacement, iteration, time and memory budgets. Recheck all quality and collision conditions; fail when limits are exhausted.
- **T10:** Define compatibility checks for deformation versus remesh. Apply updates, record chosen path and rerun the full acceptance gates. Exercise repeated runs, incompatible features and resource failure.
- **T11:** Canonicalize all semantically relevant cache inputs and versions. Implement dependency-aware invalidation and safe failure handling. Mutate each key component and compare fresh with cached outcomes.
- **T12:** Define per-update sensitivity status and its invalidation rules. Mark unsupported derivatives unavailable across repair, branch or remesh paths. Test consumer-facing status and reject misleading gradient claims.
- **T13:** Freeze the numerical acceptance contract and arrange independent held-out access. Import meshes into the pinned solver; run all cases at three refinement levels and a baseline. Publish convergence, robustness, failed cases and threshold comparisons without implying physical validation.
- **T14 (optional):** Obtain independent measurements, use permissions and operating-condition uncertainty. Preregister the application-specific physical comparison before seeing its results. Execute and review the comparison; package evidence and bounded claims only if V14 passes.
- **T15:** Assemble code, numerical evidence, licenses and distributable data with provenance. Have an independent user reproduce installation, meshing and numerical checks. Review maintainers, support and security policy; approve a numerically verified library release without experimental claims.

## Phase entry and exit gates

- **P0 contract/reuse:** Entry: stakeholder and domain reviewers available. Exit: T01–T02 approved; family, sealed hold-out procedure, feasible single topology and adoption decision recorded. Exploratory comparisons may inform decisions but are never acceptance evidence. If reuse wins, stop or adapt instead of creating a duplicate.
- **P1 geometry/topology/export:** Entry: P0 approves build/adaptation and rights. Exit: T03–T05 pass; deterministic block/periodic and independent roundtrip fixtures reviewed.
- **P2 viscous quality:** Entry: P1 passes. Exit: T06–T09 pass, adversarial failures are explicit and no invalid mesh is accepted.
- **P3 optimization:** Entry: P2 passes. Exit: T10–T12 pass for frozen update sequences and budgets; sensitivity limitations published.
- **P4 solver/refinement:** Entry: P3 passes; numerical acceptance solver, corpus, thresholds and independent held-out procedure frozen. Exit: T13 passes including held-out robustness, solver ingestion and refinement; this is not a physical accuracy or validation claim.
- **P4E optional application assessment:** Entry: T13, suitable independent measurements and permissions; freeze case-specific physical thresholds before acceptance. Exit: T14 passes with documented uncertainties and claim scope. Missing data blocks P4E and physical claims only.
- **P5 packaging:** Entry: P4 passes and rights for distributed assets/maintainers secured; P4E is not required. Exit: T15 passes externally; release review approves numerical evidence, reproducibility, provenance and support policy.
- **Future F1, 3D without clearance:** Entry: P5 plus new 3D topology/benchmark contract, endwall treatment, hex Jacobian and seam tests, and approved funding. Exit: independent 3D refinement and validation gates, not inferred from 2D.
- **Future F2, clearance:** Entry: F1 exit plus tip-gap-specific topology, leakage metrics, geometry/flow ranges and new thresholds. Exit: independently validated clearance cases. Neither future phase is authorized by this draft.
