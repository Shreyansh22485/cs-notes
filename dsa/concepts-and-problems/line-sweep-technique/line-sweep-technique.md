# Line Sweep Technique

It's like a line that sweeps across the problem space. At each point, we process the events at that point and update our answer. 
- *Line(view) moves in sorted fashion*
- *Focus on what's on the line*
- **Way of Thinking**


## Events

In Line Sweep, an event is a point where something changes and you act on it.

Line Sweep only cares about those events and nothing else.

**Sort Events and Process in Order**


## How to Apply?
1. **Identify Events**: What are the critical points where something changes?
2. **Define Events**: What data structure do I need to store events?
3. **Sort Events**: Sort events by the sweeping dimension (usually x or y).
4. **Sweep and Process**: Move the line and update the answer based on events.

### Delta
Delta is the change that happens at an event. 

## Types of Line Sweep
1. Vertical Line Sweep
    - Sweeping a Vertical Line Across the Problem Space
    - Events are at x-coordinates

2. Horizontal Line Sweep
    - Sweeping a Horizontal Line Across the Problem Space
    - Events are at y-coordinates

## When to use Line Sweep

1. Overlapping Intervals
2. Scheduling problems
3. Geometrical shape problem
4. Area/Skyline problems

---

### Line Sweep vs Difference Array

Difference Array Technique (DAT) is a specific, simplified implementation of line sweep, typically used for range updates and point queries in one dimension.

They might sound different, but they have the same core idea.

*DAT is a special case of line sweep.*
