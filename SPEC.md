# Viscous meshing library specification

**Status:** draft, 2026-11-03. Tests NOT RUN; no implementation exists as a result of this document. [Architecture](ARCHITECTURE.md) · [Plan](IMPLEMENTATION_PLAN.md) · [Verification](VERIFICATION_PLAN.md) · [Evidence](EVIDENCE.md).

## Objective and boundary

Test the hypothesis that a standalone library can repeatedly mesh a bounded, changing family of two-dimensional linear blade cascades for optimization, with stable boundary identity and explicit failure reporting. P0 must establish whether reuse already meets this need before a new engine is authorized. Grid quality is not aerodynamic accuracy. No global novelty is claimed.

V1 targets one closed, simple blade contour inside a rectangular, translationally periodic single-passage domain, with conformal linear quadrilaterals. A four-block O-grid is a **feasibility hypothesis**, not an established product requirement: P0 tests its seams and feature constraints and selects one explicit topology family or revises the design before implementation. The family contract fixes allowable parameter ranges, contour representation, pitch, domain, landmark rules, units and flow cases. Being inside parameter bounds alone does not guarantee meshability: geometry and quality checks still apply. No arbitrary CAD, multi-element blades, rotational periodicity, high-order elements or 3D in v1. A mesh cannot guarantee y+ without a flow solution; topology changes, repair branches and remeshing are not differentiable promises.

## Requirements and traceability

Each requirement is a mandatory criterion for its stated scope; R14 applies only to the optional experimentally assessed application-case package and physical claims. IDs map to the same-numbered task and test in the linked plans.

| ID | Requirement | Task / test |
|---|---|---|
| MESH-R01 | Record exploratory runs as non-acceptance without held-out access; freeze a versioned test contract and applicable numerical or physical thresholds before each acceptance run. Preserve changes and block threshold laundering. | T01 / V01 |
| MESH-R02 | Compare reuse, adaptation and new build against the same bounded contract and license constraints; document a reversible go/no-go decision. | T02 / V02 |
| MESH-R03 | Reject nonfinite, dimensionally invalid, open, self-intersecting, degenerate or out-of-family geometry with localized diagnostics. | T03 / V03 |
| MESH-R04 | Construct the single P0-selected topology family with conformal seams, explicit feature/branch constraints and paired translational periodic boundaries with stable identities; reject unsupported cases. | T04 / V04 |
| MESH-R05 | Export true 2D SU2 mesh and metadata, preserving orientation, boundary names, connectivity and periodic pairing through independent roundtrip. | T05 / V05 |
| MESH-R06 | Honor feasible first wall-to-node normal height, layer count and growth constraints; report realized spacing and infeasibility, never promise y+. | T06 / V06 |
| MESH-R07 | Detect wall, neighboring-layer, passage and periodic-image collisions; fail explicitly without exporting a mesh as valid. | T07 / V07 |
| MESH-R08 | Require positive bilinear-cell Jacobian over every cell, non-overlap and complete boundary coverage; report quality metrics. | T08 / V08 |
| MESH-R09 | Bound smoothing and repair by iteration, displacement and time budgets; revalidate and fail closed when exhausted. | T09 / V09 |
| MESH-R10 | Updates choose deformation or full remesh explicitly, rerun all gates, and provide reproducible results or explain nondeterminism and budget failures. | T10 / V10 |
| MESH-R11 | Cache keys include all semantic inputs and algorithm versions; changed dependencies invalidate affected artifacts, never return stale output. | T11 / V11 |
| MESH-R12 | Expose sensitivity capability and invalidity at each update; make no gradients-through-remesh or branch-change claim. | T12 / V12 |
| MESH-R13 | On frozen training and held-out cases, verify solver convergence and systematic refinement against preregistered numerical thresholds and a baseline. | T13 / V13 |
| MESH-R14 | For optional experimental application claims, compare measured observables and uncertainties only with rights-cleared independent data; absent evidence blocks those claims, not library release. | T14 / V14 |
| MESH-R15 | Gate numerical library release on R01–R13, license and distributed-data rights, governance, clean-install and independent reproduction, without requiring R14. | T15 / V15 |

## Open decisions

The prospective maintainers and a CFD domain reviewer must select a feasible topology, family limits and a reuse decision before P0 exits. Solver configuration and applicable acceptance thresholds must be approved before the relevant acceptance run, not before exploratory work. A designated maintainer and legal reviewer must settle code license, dependency obligations and rights for distributed data before P5. None is assigned or approved yet; these are blockers, not implicit defaults.
