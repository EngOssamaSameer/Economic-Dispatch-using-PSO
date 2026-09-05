
\[
30 \leq P_1 \leq 100
\]

## Cost Functions

Generator 1 operating cost:

\[
C_1(P_1) = 0.01P_1^2 + 2P_1 + 10
\]

Generator 2 operating cost:

\[
C_2(P_2) = 0.015P_2^2 + 1.8P_2 + 15
\]

The optimization objective is:

\[
\min C_{total} = C_1(P_1) + C_2(P_2)
\]

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

\[
v_{new} = wv_{old} + c_1r_1(pbest - x) + c_2r_2(gbest - x)
\]

### Position Update

\[
x_{new} = x_{old} + v_{new}
\]

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

\[
P_1 \approx 86\text{ MW}, \qquad P_2 \approx 64\text{ MW}
\]

with a total cost close to:

\[
C_{total} \approx 447.6
\]

## Learning Goals

By completing this project, you will understand how to:

- Model an optimization problem.
- Define constraints and an objective function.
- Represent a solution as a PSO particle.
- Implement personal-best and global-best behavior.
- Apply PSO to an energy-dispatch problem.
