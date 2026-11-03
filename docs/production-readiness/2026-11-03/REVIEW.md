# viscous-meshing review

## Scope and verdict

Pinned revision `1364f216120bba0c1264599b61a9de270655434f` is a **design-stage specification**, not an implemented mesher. Runtime, numerical tests and solver experiments: **NOT RUN**. The design is unusually explicit about limitations and acceptance integrity; the principal blockers are unresolved topology, benchmark, ownership and data-rights decisions, not proven code bugs.

The complete non-truncated tree lists six Markdown documents. The snapshot sampled `README.md:1-33`; targeted pinned reads covered `SPEC.md:1-35`, `ARCHITECTURE.md:1-30`, and `VERIFICATION_PLAN.md:1-37`. `IMPLEMENTATION_PLAN.md` and `EVIDENCE.md` were not read; external numerical, legal and standards claims were not independently checked. No target code or commands were executed.

## Architecture and product boundary

[Architecture:5-11](https://github.com/knarayanareddy/viscous-meshing/blob/1364f216120bba0c1264599b61a9de270655434f/ARCHITECTURE.md#L5-L11) proposes contract and geometry validation, block graph generation, spacing, smoothing, global quality and export. Four-block O-grid seams are explicitly a hypothesis, not a working algorithm. Proposed Python APIs and potential Gmsh/pyHyp reuse are described at [architecture:26-30](https://github.com/knarayanareddy/viscous-meshing/blob/1364f216120bba0c1264599b61a9de270655434f/ARCHITECTURE.md#L26-L30); these are not existing entry points. V1 scope is one bounded 2D linear cascade family, not arbitrary CAD or 3D ([SPEC:5-9](https://github.com/knarayanareddy/viscous-meshing/blob/1364f216120bba0c1264599b61a9de270655434f/SPEC.md#L5-L9)).

## Findings ledger

**VM-01 — High, owner decision; confidence high.** [SPEC:33-35](https://github.com/knarayanareddy/viscous-meshing/blob/1364f216120bba0c1264599b61a9de270655434f/SPEC.md#L33-L35) says maintainers and a CFD reviewer must select topology, family bounds and reuse, and that none is assigned or approved. Without these decisions there is no stable engineering contract or independent numerical acceptance authority. Recruit named owners and decide feasibility before promising implementation. This is a project blocker, not a running-system defect.

**VM-02 — High, unverified risk; confidence high that evidence is outstanding.** The proposed seam/anchor graph must remain noncrossing and periodic across the family ([architecture:9-11](https://github.com/knarayanareddy/viscous-meshing/blob/1364f216120bba0c1264599b61a9de270655434f/ARCHITECTURE.md#L9-L11)). No feasibility result is present in the inspected sources. An impossible or discontinuous layout would invalidate the selected family; run bounded exploratory endpoint and perturbation cases and record a reversible reuse/build decision. This is not a claim that the topology fails.

**VM-03 — Medium, owner decision; confidence high.** [Verification:7-13](https://github.com/knarayanareddy/viscous-meshing/blob/1364f216120bba0c1264599b61a9de270655434f/VERIFICATION_PLAN.md#L7-L13) requires an independent held-out custodian and frozen contract, while [SPEC:33-35](https://github.com/knarayanareddy/viscous-meshing/blob/1364f216120bba0c1264599b61a9de270655434f/SPEC.md#L33-L35) leaves reviewers unassigned. The process is a sensible design but cannot function until people, access and datasets exist. Assign custody and pre-register test thresholds before acceptance.

**VM-04 — Medium, owner decision; confidence high.** Licensing and distributed-data rights are explicitly unsettled ([SPEC:29-35](https://github.com/knarayanareddy/viscous-meshing/blob/1364f216120bba0c1264599b61a9de270655434f/SPEC.md#L29-L35)). Unresolved solver/dependency terms or benchmark permissions could prevent redistribution; request legal and data-owner approval rather than assuming use rights. Experimental validation is optional for the numerical library but required before a physical application claim.

## Five disciplines

Short supporting excerpts at the pinned links above: VM-01, “None is assigned or approved yet”; VM-02, “The candidate v1 topology is a **hypothesis**” and “P0 must test”; VM-03, “An independent custodian seals held-out cases before development”; VM-04, “settle code license, dependency obligations and rights for distributed data before P5.” These are explicit design dependencies, not evidence of running defects.

**Correctness/code:** no implementation exists to review. The design sensibly separates local positive cell Jacobians from global overlap and coverage, and prevents failed outputs being reported as valid ([verification:15,27-28](https://github.com/knarayanareddy/viscous-meshing/blob/1364f216120bba0c1264599b61a9de270655434f/VERIFICATION_PLAN.md#L15-L28)). Numerical validity and solver import remain untested.

**Automation:** proposed V01–V15 include negative controls, cache invalidation and independent reproduction ([verification:19-35](https://github.com/knarayanareddy/viscous-meshing/blob/1364f216120bba0c1264599b61a9de270655434f/VERIFICATION_PLAN.md#L19-L35)). The listed CLI examples are explicitly design sketches ([verification:37](https://github.com/knarayanareddy/viscous-meshing/blob/1364f216120bba0c1264599b61a9de270655434f/VERIFICATION_PLAN.md#L37)); do not run them as existing tools.

**DevOps:** no deployment is evidenced or necessary for a design document. A future release needs reproducible tool versions, artifact hashes, benchmark provenance and an independent install; availability and solver licensing are open.

**Security/OWASP:** no network, auth or secret-handling implementation is sampled, so web-specific vulnerabilities are inapplicable. Future file inputs and imported geometry need resource limits, input validation, safe output paths and supply-chain review; these are preventive requirements, not findings of exploitation.

**UI/UX:** no UI exists. A future library/CLI should produce actionable failure codes, locations, units and explicit non-acceptance labels; the proposed result statuses already recognize this boundary ([architecture:17-24](https://github.com/knarayanareddy/viscous-meshing/blob/1364f216120bba0c1264599b61a9de270655434f/ARCHITECTURE.md#L17-L24)). Usability is untested.

## Owner questions and limitations

Who owns the numerical contract, held-out cases, data rights and release? Which solver and geometry ranges can reviewers independently access? What compute budget and recovery of benchmark evidence are required? No hardware, solver, external licenses or datasets were accessed. No certification or aerodynamic performance is implied. See [REMEDIATION_PLAN.md](REMEDIATION_PLAN.md).
