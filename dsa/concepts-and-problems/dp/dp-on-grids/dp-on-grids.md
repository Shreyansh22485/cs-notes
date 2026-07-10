# DP on Grids

- Technique to solve problems that involve moving through a grid often a 2D Matrix
- Each position on the grid can have some
    - Some value like cost, reward etc
    - Goal like Find optimal path 
    
**Each cell -> can represent a state/subproblem**
**Key idea is to compute answer for cell (i,j) using answers of subproblems**
**These subproblems can be found by looking at the previous cells**

**Previous cells -> can be up, left, up-left (depending on allowed moves)**

### Types of Problems

1. Unique Path Count
2. Minimum/Maximum Path Sum
3. Path Exist or Not
4. Shortest Path in a Grid
5. Game Board 
6. Matrix Traversal/Walk

