---
name: reproducibility-level
description: Establish or apply agreed reproducibility requirements during system design, implementation, testing, and review.
---

# Reproducibility Level

Use this skill when establishing reproducibility requirements or applying settled reproducibility guarantees during design, implementation, testing, and review.

## Declare the required guarantee

Use the repository or task's authoritative requirements and design to establish the level (`0`–`3`). At level `0`, apply the existing behavior contract. For each required reproduction guarantee at level `1` or higher, record:

- **Target:** the output, final state, execution trace, generated artifact, statistical property, or other observable property being reproduced.
- **Conditions:** the relevant inputs, initial state, random state, versions, environment, and permitted variations.
- **Equivalence:** what counts as a match for that target, such as exact state equality, byte identity, an agreed numeric tolerance, or a defined statistical criterion.
- **Level:** the selected level (`1`, `2`, or `3`) governing this target.

Agree on material missing choices through the workflow responsible for requirements and design. Record the agreed contract in the appropriate source of truth. Different targets may use different criteria and levels.

## Levels

Levels bound the **scope of conditions** where the declared equivalence must hold. The equivalence criterion is a separate part of the contract.

| Level | Required guarantee |
| --- | --- |
| `0` | Apply existing behavior requirements; add no reproducibility guarantee. |
| `1` | Reproduce explicitly named cases under their specified conditions. |
| `2` | Reproduce the declared class of valid inputs and runs under the specified equivalent execution conditions. |
| `3` | Also reproduce across the explicitly declared variations of environment or implementation. |

Higher levels include lower-level guarantees **for the same target and equivalence criterion**. At level `2`, declare the applicable input/run class; at level `3`, declare the environment or implementation variations. Maintain the agreed level throughout the task; route proposed changes through the owning requirements/design workflow.

Exact equality for one target does not by itself guarantee identical intermediate steps, another target, or an independent statistical property. Assess each guarantee by its declared contract.

## Separate reproducibility from performance

Elapsed calculation time, CPU time, latency, throughput, and resource consumption belong to performance requirements and execution constraints. Assess them with separately specified measurement conditions and acceptance criteria.

Evaluate reproducibility using its declared target, conditions, equivalence, and level. Differences in incidental measured execution durations alone do not establish a reproducibility failure or justify stopping work.

Apply deadlines, timeouts, and execution budgets as stop criteria when the governing operational, performance, or test-execution contract explicitly establishes them. When timing is itself an explicitly required observable behavior, have requirements/design establish the relevant acceptance criterion and measurement protocol.

## Apply to work

- **Design:** express the agreed contract in the authoritative requirements or design.
- **Implementation:** preserve the guarantee within its defined conditions using mechanisms appropriate to the contract.
- **Testing:** use the governing test-evidence workflow to establish sufficient executable evidence for the guarantee.
- **Review:** identify gaps against the agreed contract and cite the target, conditions, criterion, level, and supporting evidence.

`defense-level` owns defensive scope against invalid interactions and environment failures. Test-evidence skills own test planning and implementation. Performance requirements and execution budgets own their respective limits.

This skill owns the definition and interpretation of required reproducibility guarantees.
