# Hare and Tortoise Algorithm

The Hare and Tortoise algorithm, also known as Floyd's Cycle Detection Algorithm, is a pointer algorithm that uses two pointers to detect cycles in a sequence of values. The algorithm is named after the fable of the hare and the tortoise, where the hare moves faster than the tortoise.

## How to Identify it is a Hare and Tortoise Algorithm Problem?
- Duplicacy: If the problem involves detecting duplicates in a sequence or linked list, it may be a candidate for the Hare and Tortoise algorithm.
- Cycle Detection: If the problem involves detecting cycles in a linked list or sequence, it may be a candidate for the Hare and Tortoise algorithm.
- Traverse through indices: The numbers are valid indices of the array( 1 to n)

## Algorithm
1. Initialize two pointers, `slow` and `fast`, both pointing to the head of the linked list or the starting index of the sequence.
2. Move the `slow` pointer one step at a time and the `fast` pointer two steps at a time.
3. If there is a cycle, the `fast` pointer will eventually meet the `slow` pointer. If the `fast` pointer reaches the end of the sequence (null), then there is no cycle.
4. If a cycle is detected, reset one of the pointers to the head of the linked list or the starting index of the sequence and move both pointers one step at a time until they meet again. The meeting point will be the start of the cycle.

### Proof of Correctness

Let's denote the following:
- `L`: The distance from the head of the linked list to the start of the cycle
- `C`: The length of the cycle
- `M`: The distance from the start of the cycle to the meeting point of the two pointers

When the two pointers meet, the `slow` pointer has traveled a distance of `L + M`, while the `fast` pointer has traveled a distance of `L + M + kC`, where `k` is the number of complete cycles the `fast` pointer has made.

Since the `fast` pointer moves twice as fast as the `slow` pointer, we have the equation:
$$
2(L + M) = L + M + kC
$$

Simplifying this equation, we get:
$$
L + M = kC
$$

This means that the distance from the head of the linked list to the start of the cycle is equal to the distance from the meeting point to the start of the cycle plus some multiple of the cycle length. This is the key insight that allows us to find the start of the cycle.
