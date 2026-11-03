# Viscous Meshing

Design specifications for an optimization-ready viscous meshing library for bounded aerospace geometry families.

**Status: reviewed design draft.** This repository contains specifications and implementation plans, not an implemented mesher. Planned numerical tests have not been run.

## Vision

Make repeated geometry-to-mesh workflows reproducible: preserve boundary identities, control boundary-layer spacing, detect invalid cells and explain meshing failures during design optimization.

The proposed first version targets two-dimensional linear blade cascades with a single supported topology family. Topology feasibility and reuse of existing mesh tools must be evaluated before implementation. Later three-dimensional and tip-clearance capabilities require separate verification gates.

## Documentation

| Document | Contents |
| --- | --- |
| [Specification](SPEC.md) | Scope, requirements, exclusions and open decisions |
| [Architecture](ARCHITECTURE.md) | Geometry, topology, records, interfaces and design alternatives |
| [Implementation plan](IMPLEMENTATION_PLAN.md) | Ordered tasks, dependencies and phase/task definitions of done |
| [Verification plan](VERIFICATION_PLAN.md) | Mesh checks, negative cases, refinement and acceptance protocols |
| [Evidence](EVIDENCE.md) | Primary sources, alternatives, licensing and unresolved assumptions |

## Starting point

Begin with phase P0: select a bounded geometry family, evaluate existing meshers, identify reviewers and establish the benchmark contract. The proposed four-block O-grid remains a feasibility hypothesis. Mesh quality alone does not establish aerodynamic accuracy, and a mesh alone cannot guarantee a particular y-plus value.

## Contributing

Issues and proposals concerning geometry fixtures, meshing algorithms, solver interfaces and reproducible benchmarks are welcome. Reference requirement/task IDs and distinguish implemented evidence from proposed capability. Changes to acceptance criteria must retain prior results and their original thresholds.

## Licensing

An open-source release is intended; a license has not yet been selected. Public visibility alone does not grant an open-source license. Upstream software and benchmark data retain their own terms; resolve compatibility and redistribution rights in P0.
