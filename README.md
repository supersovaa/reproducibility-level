# Reproducibility Level

A lightweight skill for a single user and an AI agent to agree on and apply the reproducibility required of a system.

Use `reproducibility-level` when establishing reproducibility requirements, or applying settled reproducibility guarantees during design, implementation, testing, and review.

## Contract

For each required guarantee, declare:

- **Target:** what is reproduced (for example, a game state, execution trace, build artifact, or statistical property).
- **Conditions:** the inputs and execution conditions under which it is reproduced.
- **Equivalence:** what counts as the same result, including any agreed tolerances or statistical criteria.
- **Level:** the breadth of conditions covered by the guarantee.

| Level | Scope |
| --- | --- |
| `0` | Existing behavior requirements only; no additional reproduction guarantee |
| `1` | Explicitly named cases under specified conditions |
| `2` | Declared class of valid inputs and runs under equivalent conditions |
| `3` | Also includes declared variations in environment or implementation |

Higher levels include lower ones for the same target and equivalence criterion. An exact result match, exact execution trace, numerical tolerance, and statistical acceptance represent different contracts rather than a universal ladder of strictness.

### Example

```text
Use reproducibility-level with:
  target: state after each turn
  conditions: same rules, initial state, action sequence, and random state
  equivalence: exact equality of the contracted game state
  level: 1
  cases: the explicitly specified replay scenarios
```

Level `2` would require defining a class of valid inputs and runs to cover, while level `3` additionally names the supported environment or implementation differences.

## Timing and performance

Reproducing a calculation's result does not imply equal elapsed execution time. Calculation time, latency, and throughput are evaluated using separately agreed performance requirements.

Differences in incidental calculation duration alone are not a reproducibility failure or a reason to stop a task. Explicit operational timeouts and test budgets remain applicable when declared by their owning requirements.

## Installation

Place the root `SKILL.md` in the skill directory used by your AI agent or skill loader, such as `<skills-root>/reproducibility-level/SKILL.md`. In the repository's governing instructions, invoke the skill for reproducibility decisions and for checking settled guarantees. Store each agreed contract with the relevant requirements or design.

## Responsibilities

This skill owns reproducibility guarantees. [defense-level](https://github.com/supersovaa/defense-level) owns defensive scope; [requirement-driven-testing](https://github.com/supersovaa/requirement-driven-testing) owns executable test evidence; performance requirements and test-execution budgets own their corresponding limits.

See [SKILL.md](SKILL.md) for operational rules.
