# 1-D Dynamic Programming

1-D dynamic programming is a technique used to solve optimization problems by breaking them down into simpler subproblems and storing the results of these subproblems to avoid redundant calculations. It is particularly useful when the problem has overlapping subproblems and optimal substructure properties.

## Recurrence Relation or Recursion Tree Diagram

- The recurrence relation is a mathematical expression that defines the solution to a problem in terms of the solutions to smaller subproblems. It captures the relationship between the current state and its previous states.

- Time Complexity of recursion tree is O(2^n) in the worst case, as each function call can lead to two more calls, resulting in an exponential growth of the number of calls.

## Implementation Approaches

There are two main approaches to implementing 1-D dynamic programming solutions:

1. **Top-down (Memoization)**: This approach uses recursion with a cache to store the results of subproblems.
2. **Bottom-up (Tabulation)**: This approach builds the solution iteratively from the base cases upwards.

### Top-down (Memoization) Approach

The state is defined by the parameters of the recursive function, and the memoization table stores the results of previously computed subproblems to avoid redundant calculations.

**Base Case**: The simplest case that can be solved directly without further recursion. It's usually the result for the lowest possible value of the input parameter.

- The time complexity of the top-down approach is O(n) because each subproblem is solved only once and stored in the memoization table.
- The space complexity is O(n) for the memoization table and O(n) for the recursion stack, leading to a total space complexity of O(n).

### Bottom-up (Tabulation) Approach

The bottom-up approach involves filling up a table iteratively based on the base cases and the recurrence relation. It avoids recursion and builds the solution from the ground up.

**State Definition**: The meaning of dp[i] is defined based on the problem being solved. It typically represents the optimal solution for a subproblem of size i.

**Base Case**: The initial values of the dp array that represent the simplest subproblems.

- The time complexity of the bottom-up approach is O(n) because it iteratively computes the solution for each subproblem.
- The space complexity is O(n) for the dp array, but it can often be optimized to O(1) if only a fixed number of previous states are needed to compute the current state.

### Space Optimization

In many 1-D dynamic programming problems, the current state only depends on a fixed number of previous states. This allows for space optimization by using a rolling array or a few variables instead of maintaining the entire dp array.