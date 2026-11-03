# viscous-meshing remediation plan

This roadmap implements the existing design's gates rather than pretending code defects exist. Review: [REVIEW.md](REVIEW.md). All commands, files beyond those listed, experiments and deployments below are proposed and not executed.

| Phase | Task | Entry → exit |
|---|---|---|
| P0 | VM-T1 | Named sponsor → bounded, reviewed reuse/topology decision. |
| P1 | VM-T2 | P0 contract → isolated implementation and independent negative cases. |
| P2 | VM-T3 | Candidate available → frozen numerical acceptance and independent reproduction. |
| P3 | VM-T4 | Numerical evidence and rights → owner-authorized release decision. |

## VM-T1 — Establish family, custody and feasibility (VM-01, VM-02, VM-03)

**Prerequisites:** sponsor and CFD reviewer available. **Observed paths:** `SPEC.md`, `ARCHITECTURE.md`, `VERIFICATION_PLAN.md`; proposed family contract and exploratory records. **Steps:** (1) Assign maintainer, independent reviewer and held-out-data custodian; record authority and separation of access. (2) Define units, geometry limits, features, periodic domain and exploration corpus; keep held-out cases sealed. (3) Compare available reuse against new build on the same contract, including difficult seams, endpoint geometries and perturbations; document version, failure and license constraints. **Deliverable:** signed go/no-go decision with selected topology or explicit revision. **Verification:** a reviewer repeats representative cases without acceptance claims and checks rejected alternatives and unknowns.

- [ ] The geometry family and ownership are explicit and reviewable.
- [ ] Feasibility failures and unavailable alternatives are retained, not hidden.
- [ ] Held-out cases are inaccessible to exploratory developers.

## VM-T2 — Implement failure-closed mesh generation (VM-02; preventive correctness/security)

**Prerequisites:** T1 selects an approach. **Paths:** observed `ARCHITECTURE.md:7-30`; proposed library, test and fixture paths to be chosen after stack decision. **Steps:** (1) Implement contract validation and explicit diagnostics for invalid geometry and resource limits, then topology generation with stable seam and boundary identities. (2) Add independent checks for cell orientation, folded cells, overlap, collision and complete domain coverage; never expose diagnostic meshes as valid solver inputs. (3) Implement SU2 export and sidecar with a separately authored reader roundtrip, then verify cache invalidation and update branches. **Deliverable:** a bounded implementation with tests and recorded dependencies. **Verification:** deliberate inversion, seam mismatch and stale cache mutations must each make a relevant test fail.

- [ ] Unsupported or invalid input produces a localized failure, not an OK mesh.
- [ ] Independent export reader checks names, connectivity, orientation and periodic pairing.
- [ ] Inputs and outputs obey approved memory, time and path constraints.

## VM-T3 — Numerical acceptance with independent data custody (VM-03)

**Prerequisites:** T2 candidate; independent custodian and frozen solver configuration. **Paths:** observed `VERIFICATION_PLAN.md:5-35`; proposed signed contract, corpus manifest and run logs. **Steps:** (1) Freeze metrics, limits, candidate hash, geometry manifest, solver versions and failure policy before releasing held-out inputs. (2) Run three systematically refined levels and record convergence, mass balance, output quantities, y-plus distribution and failures against the approved baseline. (3) Have a non-author reproduce in a separate environment, keeping exploratory and acceptance records distinct; invalidate a reused holdout after adaptive changes. **Deliverable:** signed numerical evidence with failures and uncertainty. **Verification:** a modified contract and intentionally bad cell must be rejected, and an independent solver import must observe expected boundary markers.

- [ ] Thresholds and corpus hashes predate each acceptance run.
- [ ] All held-out failures remain visible; no post-result threshold laundering.
- [ ] Independent reproduction and solver convergence are observed, not inferred.

## VM-T4 — Rights, release and recovery (VM-04)

**Prerequisites:** T3 and designated legal/maintainer owners. **Paths:** observed `SPEC.md:29-35`, `README.md:23-25`; proposed license inventory, signed release and archive. **Steps:** (1) Obtain written rights for code, dependencies and distributed benchmark data, and record limitations on any experimental datasets. (2) Produce a versioned release with provenance and clean-install instructions, reviewed by a non-author. (3) Archive inputs, contracts and results with an owner-approved retention/restore process; keep experimental validation separate unless independent measurements are authorized and assessed. **Deliverable:** release decision and recovery record. **Verification:** restore the archive into an isolated location and independently reproduce representative evidence.

- [ ] Licenses and data distribution permissions are approved.
- [ ] An independent install and evidence restore are observed.
- [ ] Claims distinguish numerical verification from physical validation.

## Acceptance and approval policy

Release is blocked by missing topology selection, numerical evidence, ownership or applicable rights; physical-application claims additionally need independent experimental evidence. The owner must approve data access, solver costs, licenses and any public release. Preserve old contracts and results when revising thresholds; revert releases via versioned artifacts without deleting failed evidence. No CI, deployment or tests are represented as already available.
