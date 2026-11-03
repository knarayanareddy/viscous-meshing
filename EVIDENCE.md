# Evidence and adoption record

**Draft · 2026-11-03. Tests NOT RUN.** Six primary-source pages read on 2026-11-03; upstream statements are documentation claims, not locally tested behavior. No code, benchmark, install or solver run was performed. See [spec](SPEC.md), [plan](IMPLEMENTATION_PLAN.md) and [verification](VERIFICATION_PLAN.md).

| Source | Supported observation and limitation |
|---|---|
| [pyHyp repository](https://github.com/mdolab/pyhyp) | README says hyperbolic marching extrudes structured surface meshes, generally sourced from ICEM, for optimization preprocessing. It is a serious reuse candidate, not evidence of an unmet global need. |
| [Turbomesh repository](https://github.com/pascalPost/turbomesh) | README lists boundary layers, automated blocking and cascades in a roadmap; that list neither proves implementation nor proves absence. The repository declares AGPL-3.0; assess exact reuse obligations. |
| [Gmsh reference manual](https://gmsh.info/doc/texinfo/gmsh.html) | Documents structured/unstructured meshing, periodic facilities, APIs and physical groups; documented output-group behavior makes marker roundtrip important. Its licensing and actual fit need review. |
| [SU2 mesh documentation](https://su2code.github.io/docs_v7/Mesh-File/) | Describes true 2D mesh coordinates, element connectivity and named boundary markers; periodic transform metadata must be conveyed and checked separately. |
| [SU2 turbomachinery guide](https://su2code.github.io/docs_v7/Setup-Guide-Turbomachinery/) | Draft guide describes blade-passage periodic configuration and recommends convergence checks; it is not validation of our future configuration. |
| [NASA CFD Vision 2030, 2014](https://ntrs.nasa.gov/citations/20140003093) | Historical strategic report identifies CFD capability challenges; it does not establish a present-day gap or novelty. NASA notes portions may be copyright protected. |

## Adoption and governance

P0 produces a decision matrix for reuse as-is, adapter/upstream contribution, fork, or standalone implementation, including engineering effort, exploratory contract fit, API and license implications. Exploration is non-acceptance and cannot use held-out cases. Prefer the least duplicative option satisfying the approved family contract; four-block O-grid feasibility remains unproven. Propose a public maintainer group with domain and software reviewers, transparent issue triage, review and release policy, documented support boundaries and a private security-contact process. Start with a reproducible research prototype, invite independent users to review the benchmark, then consider stable API releases only after P5. No project, license, contributor agreement or governance body is established yet.

**Library-release blockers:** named maintainers and domain approvers; approved family, numerical acceptance corpus and thresholds; approved solver setup; rights to distributed assets; compatible code/dependency licenses; independent reproducer. **Optional physical-claim blockers:** independent measured data, permission to use it, uncertainty information and preregistered physical thresholds. If data cannot be shared, document permitted access-controlled reproduction; without adequate data, the optional case package and accuracy claims remain blocked, not P4/P5 library release. Source availability alone does not grant data redistribution rights.
