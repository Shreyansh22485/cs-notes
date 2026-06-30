# Difference Array Technique

Famous technique use to efficiently apply range updates on an array.
It helps to do multiple range updates in constant time O(1).

**Ideal for Range Modifications and Querying**

## Working:

Let's consider an array arr of size n.
We create a difference array diff of size n+1 and initialize it with zeros.

For each update of the form: add x to the range [l, r]
We simply do:
```cpp
diff[l] += x;
diff[r+1] -= x;
```

- After all updates are done, we can reconstruct the final array by taking the **prefix sum** of the difference array.

## Example:

```cpp
// Initial array
arr = [0, 0, 0, 0, 0]

// Updates
update(1, 3, 2);  // Add 2 to range [1, 3]
update(2, 4, 3);  // Add 3 to range [2, 4]

// Difference array after updates
diff = [0, 2, 3, 0, -5, 0]

// Final array after prefix sum
final_arr = [0, 2, 5, 5, 0, 0]
```

## Time Complexity:

- Range updates: O(1)
- Reconstructing the final array: O(n)

## Segment Tree vs Difference Array:

| Feature | Difference Array | Segment Tree |
|---|---|---|
| Time Complexity | O(1) range updates, O(n) reconstruct | O(log n) for both range updates and queries |
| Space Complexity | O(n) | O(4*n) |
| Use Cases | Range updates, no point queries | Range updates and range queries |

### When to use:

- Difference Array
    - Best suited for problems where you need to perform multiple range updates
    - you don't need to query the array in between the updates.
    - you only need to query the final array after all the updates are done.

- Segment Tree
    - Best suited for problems where you need to perform multiple range updates and range queries
    - you need to query the array in between the updates.

## Leetcode problems:

- [LC2381. Shifting Letters II](problems/LC2381.%20Shifting%20Letters%20II.md)
- [LC3355. Zero Array Transformation I](problems/LC3355.%20Zero%20Array%20Transformation%20I.md)
- [LC3356. Zero Array Transformation II](problems/LC3356.%20Zero%20Array%20Transformation%20II.md)
