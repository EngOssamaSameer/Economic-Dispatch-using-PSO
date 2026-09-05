# Particle Swarm Optimization for Economic Dispatch

## Overview

This project applies **Particle Swarm Optimization (PSO)** to a simple Economic Dispatch problem. The objective is to distribute an electricity demand between two generators while minimizing the total operating cost.

## Problem Statement

Two generators must satisfy a total electricity demand of **150 MW**.

The solution must:

- Meet the total demand.
- Respect each generator's minimum and maximum operating limits.
- Minimize the combined operating cost.

The total power generated must equal the total demand:

```text
P1 + P2 = 150
```

Where:

- `P1` is the power produced by Generator 1.
- `P2` is the power produced by Generator 2.

Once `P1` is selected, calculate Generator 2 output as:

```text
P2 = 150 - P1
```

Example: if `P1 = 80`, then `P2 = 150 - 80 = 70`.

## Generator Constraints

| Generator | Minimum Output | Maximum Output |
|---|---:|---:|
| Generator 1 | 20 MW | 100 MW |
| Generator 2 | 30 MW | 120 MW |

Because `P2 = 150 - P1`, the valid search range for `P1` is:

```text
30 <= P1 <= 100
```

## Cost Functions

Generator 1 cost is calculated from its generated power:

```text
C1 = 0.01 * P1**2 + 2 * P1 + 10
```

Generator 2 cost is calculated the same way:

```text
C2 = 0.015 * P2**2 + 1.8 * P2 + 15
```

The total cost is the sum of both costs:

```text
total_cost = C1 + C2
```

The goal is to find the values of `P1` and `P2` that produce the **smallest `total_cost`**.

### Calculation Example

For `P1 = 80`:

```text
P2 = 150 - 80 = 70
C1 = 0.01 * 80**2 + 2 * 80 + 10 = 234
C2 = 0.015 * 70**2 + 1.8 * 70 + 15 = 214.5
total_cost = 234 + 214.5 = 448.5
```

## PSO Design

Each particle represents one possible value of \(P_1\).

Each particle stores:

- `position`: Current proposed value for `P1`.
- `velocity`: Direction and size of its next movement.
- `personal_best_position`: Best solution found by that particle.
- `personal_best_cost`: Cost of its personal best solution.

The swarm also keeps:

- `global_best_position`: Best solution found by all particles.
- `global_best_cost`: Lowest cost found by all particles.

### Velocity Update

```text
new_velocity =
    (w * current_velocity)
    + (c1 * r1 * (personal_best_position - current_position))
    + (c2 * r2 * (global_best_position - current_position))
```

### Position Update

```text
new_position = current_position + new_velocity
```

Suggested starting parameters:

| Parameter | Value | Purpose |
|---|---:|---|
| `w` | 0.7 | Keeps part of the previous movement. |
| `c1` | 1.5 | Learning from the particle's own best solution. |
| `c2` | 1.5 | Learning from the swarm's best solution. |

## Project Structure

```text
project/
├── main.py          # PSO implementation
└── README.md        # Project documentation
```

## Expected Output

After running the program, it should print:

- Best output for Generator 1 (`P1`).
- Corresponding output for Generator 2 (`P2`).
- Minimum total operating cost.

For this example, the expected optimal distribution is approximately:

```text
P1 ≈ 86 MW
P2 ≈ 64 MW
```

with a total cost close to:

```text
total_cost ≈ 447.6
```

## Learning Goals

By completing this project, you will understand how to:

- Model an optimization problem.
- Define constraints and an objective function.
- Represent a solution as a PSO particle.
- Implement personal-best and global-best behavior.
- Apply PSO to an energy-dispatch problem.
