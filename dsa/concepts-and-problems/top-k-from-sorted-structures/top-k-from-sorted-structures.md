# Top K Elements from Sorted Structures Pattern

This pattern involves finding the top K elements from sorted structures such as arrays, linked lists, or binary search trees. The key idea is to leverage the sorted nature of the data structure to efficiently retrieve the top K elements.

## Heap-based Approach (for unsorted inputs)
- Kth Smallest
    - Use a max-heap of size K to keep the K smallest elements seen so far.
    - Iterate through the elements and push each into the heap. If the heap size exceeds K, pop the maximum (root) to discard larger elements.
    - After processing all elements, the root of the max-heap is the Kth smallest element.
- Kth Largest
    - Use a min-heap of size K to keep the K largest elements seen so far.
    - Iterate through the elements and push each into the heap. If the heap size exceeds K, pop the minimum (root) to discard smaller elements.
    - After processing all elements, the root of the min-heap is the Kth largest element.
- Top K
    - General approaches:
        - Use a heap of size K (min-heap to keep K largest, max-heap to keep K smallest).
        - Use Quickselect to find the Kth element (average O(n)) then take partitioned top K.
        - For already-sorted inputs, pick the K elements directly (index-based).
- Best K
    - Interpreted as "top K by a custom score or frequency":
        - For custom comparator: maintain a heap of size K using the comparator to keep the best K items.
        - For top K frequent: build a frequency map, then use a heap of size K (or bucket sort) to retrieve the most frequent elements.
- Merge K Sorted Lists
    - Use a min-heap that stores the current head node/value from each list.
    - Repeatedly pop the smallest, add it to the result, then push the next element from that list.
    - Time complexity O(N log K) where N is total elements and K is number of lists; space O(K).
- Sorted rows in 2D Matrix -> Find top k
    - If each row is sorted (ascending): treat rows as K sorted arrays and use the Merge K Sorted Lists pattern with a heap of row heads.
    - If the whole matrix is row- and column-sorted, you can also use a min-heap seeded with the first element of each row or use binary search on value range with a counting step (LeetCode 378 style) to find the Kth smallest.
- Sorted columns in 2D Matrix -> Find top k
    - Symmetric to the row-based approach: treat columns as sorted lists and merge using a heap, or use binary-search-on-values if rows+columns are both sorted.
- Pair Sums -> Find top k
    - Given two sorted arrays A and B (descending for largest sums):
        - Use a max-heap seeded with pairs (A[i]+B[0], i, 0) for i in [0..min(K-1, len(A)-1)].
        - Pop the largest sum (i, j) and push (i, j+1) if j+1 < len(B), avoiding duplicates with a visited set.
        - Complexity O(K log K).

### Check:
- Avoid generating all possibilities
- can Heap help? (Yes, often)
- I only care about the next best (smallest/largest)
    