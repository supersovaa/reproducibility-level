---
name: reproducibility-level
description: Establish or apply agreed reproducibility requirements during system design, implementation, testing, and review.
---

# Reproducibility Level

Use this skill in a single-user, AI-agent workflow when establishing reproducibility requirements or applying settled guarantees during design, implementation, testing, and review.

## Declare the contract per target

Use the task or repository's authoritative requirements and design for existing behavior and reproduction contracts. For each relevant reproduction target, identify:

- **Target:** the output, result, state, recorded data, numerical value, or statistical property under consideration.
- **Axis and level:** select only the logical, numerical/data, and statistical axes relevant to this target, with their applicable level. A deliberately selected level `0` means no additional reproducibility requirement for that target and axis; it preserves existing behavior requirements.
- **Conditions and equivalence, when applicable:** for an axis with a required assessment or guarantee, use the owning contract's inputs, initial state, recorded decisions, random state or seeds, code/data versions, permitted environmental variations, and agreed matching or assessment criterion. At level `0`, preserve any existing conditions and behavior criteria without requiring a new reproducibility equivalence criterion.

Record agreed axis/level selections in the consuming repository's chosen authoritative location, such as a local task `SKILL.md`; reference the owning requirements/design for the substantive target guarantee, conditions, and equivalence. Different targets can have different axes, levels, conditions, and equivalence criteria. A higher number flags greater risk of overconstraining legitimate behavior; it does not generally imply mathematical containment or increasing precision. Apply a guarantee only within the agreed contract. Route material proposals for new or changed guarantees to the workflow that owns requirements and design.

## Logical reproducibility

| Level | Interpretation |
| --- | --- |
| `0` | No additional logical reproduction guarantee. |
| `1` | **Input/output agreement:** under the same contracted input sequence and execution conditions, reproduce the output sequence or final result specified by the owning contract. |
| `2` | **Internal execution-path agreement:** retain level-`1` input/output agreement and additionally reproduce the internal processing path explicitly identified by the owning contract, using its agreed equivalence criterion. |

The owning contract identifies which outputs must agree. Semantically observable state transitions or recorded events can be outputs when explicitly part of that contract; agreement of the internal algorithm or instruction path is a distinct level-`2` requirement. For level `2`, require an agreed path target and comparison rule rather than imposing universal instruction order, scheduling, search paths, or execution traces. Preserve implementation and parallelization freedom at level `1`.

## Numerical and data reproducibility

| Level | Interpretation | Role |
| --- | --- | --- |
| `0` | No additional numerical/data reproducibility requirement. | Selection |
| `1` | **Order-of-magnitude assessment:** assess similarity of scale or magnitude. | Assessment |
| `2` | **Approximate assessment:** assess broad agreement at an agreed rounding precision or comparable approximate criterion. | Assessment |
| `3` | **Discrete agreement:** guarantee equality of values originally specified as discrete, such as integers, identifiers, or contractual byte sequences. | Guarantee |
| `4` | **Toleranced agreement:** guarantee numerical agreement within expressly agreed absolute, relative, or other tolerances. | Guarantee |
| `5` | **Full numerical representation identity:** a prohibited requirement boundary for bit-identical internal numerical representations such as floating-point computation results. | Do not require |

Levels `3` and `4` are parallel contracts, not a strictness ladder. Level `4` is numbered later to highlight the risk of selecting an unjustifiably small tolerance. Set tolerances from the required precision, value scale, numerical behavior, and owning specification; level `4` alone specifies no universal epsilon.

Distinguish assessment from a required guarantee: rounding an originally continuous value for comparison is level `2`, whereas a promised bound is level `4`. Contractual discrete values, including byte sequences defined as published data values, may require level `3` equality. Do not reinterpret a numerical implementation's internal floating-point bits as contractual discrete data to bypass the level-`5` boundary.

## Statistical reproducibility

| Level | Interpretation |
| --- | --- |
| `0` | No additional statistical reproducibility requirement. |
| `1` | Assess the similarity of agreed statistics or statistical trends. |
| `2` | Guarantee statistical equivalence under pre-agreed sample composition/count, tolerances, and acceptance criteria. |

For statistical levels `1` and `2`, name the statistics of interest (for example mean, rate, dispersion, quantile, or distribution) separately from the level. Level `0` preserves existing statistical behavior without introducing a new evaluation target. For level `2`, let the owning requirements/design and test-evidence planning define the sample size, sampling/seed conditions, tolerances, decision procedure, and any needed confidence or power. Treat finite-sample variation according to that contract. The level `2` designation alone does not require a large random experiment in ordinary CI. Fixed sample data and deterministic aggregation tests can provide evidence when they fit the agreed test objective.

## Apply the owning execution conditions

Randomness is a condition shared by the three axes, rather than a fourth axis. Distinguish a random stream, outcomes of a random process, and statistics over trials as separate targets where needed.

- Follow the consuming system's normal execution contract for explicit seeds, omitted seeds, generated seeds, and defaults. Reproducibility alone does not change normal runs to a fixed default seed.
- For comparison or replay, apply the seeds, inputs, recorded choices, versions, and other conditions required by that target's existing reproduction contract. A selected seed `s` may be supplied to both runs when the contract calls for comparison at that value; do not infer that normal runs must use the same fixed `s`.
- A matching seed may guarantee initial state or derived random allocations only. Match the actual contract before requiring the same later decisions, execution path, or final outcome; random-number consumption, parallelism, external decisions, and recorded inputs can affect that scope.
- Use the existing contract to determine legitimate omissions, defaults, record versions, and the range of comparable results. When comparisons cover a limited range, state that range and its basis; route a proposed additional guarantee to the owning design workflow. Do not introduce skill-specific fallback execution paths or preconditions.

## Separate reproducibility from performance and test selection

Elapsed time, CPU time, latency, throughput, and resource consumption belong to the owning performance requirements and execution budgets. Incidental timing differences alone do not establish reproducibility failure or justify stopping work. Apply a timing acceptance rule only when its own operational or performance contract defines it.

- **Design:** maintain substantive reproduction guarantees, conditions, and equivalence in the owning requirements/design; record agreed axes and levels in the consuming repository's chosen authoritative location, with references to those contracts.
- **Implementation:** preserve the agreed guarantees within their defined scope.
- **Testing:** use the existing test-evidence workflow to select sufficient evidence, workload, CI placement, and budget for the contracted guarantee.
- **Review:** compare behavior with the existing contract and, when an assessment or guarantee applies, compare the evidence with its agreed target, conditions, equivalence, and level. Identify concrete contract gaps rather than imposing broader guarantees.

This skill owns interpretation of reproducibility guarantees. `defense-level` owns defensive scope, test-evidence skills own testing choices, and performance/operational contracts own their limits.

## Migrate existing level settings

The former single `0`–`3` level system measured the breadth of cases, valid inputs, and environment variations. Re-evaluate each existing target using its authoritative behavior and reproduction contract, including conditions and equivalence criteria where applicable, then select the relevant axes and levels in this skill. Preserve existing guarantees during this review. Do not automatically map old numbers to new numbers.
