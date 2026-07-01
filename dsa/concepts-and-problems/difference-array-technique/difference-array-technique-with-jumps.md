# Difference Array Technique with Jumps

This variation of difference array technique is used to apply range updates on an array where the updates are applied on indices that are k distance apart.

## Working:

Let's consider an array arr of size n.
We create a difference array diff of size n+1 and initialize it with zeros.

For each update of the form: add x to the range [l, r] with a jump of k
```cpp
diff[l] += x;
steps = (r-l)/k; // Steps within [l,r]
next = l + (steps+1)*k;

diff[next] -= x;
```

Then we calculate the final array by taking the **prefix sum** by jumping k steps:
```cpp
for(int i = 0; i < n; i++){
    if(i-k >= 0)
        diff[i] += diff[i-k];
}
```
We need to club all queries with same k, so that we can perform the above cummulative sum of the diff array and then update the nums. Then we do a new iteration for the next value of k 

**Note:** 
- If there are multiple Ks, group queries for each K and handle their queries at once.
    - k -> {Q1,Q2,Q3} -> DAT -> nums
    - k`-> {Q4,Q5,Q6} -> DAT -> nums
    - ...

## What if Query asks for multiplication of val

- Diff array is initialized with 1 instead of 0
- For each update of the form: multiply x to the range [l, r] with a jump of k
```cpp
diff[l] *= x;
steps = (r-l)/k; // Steps within [l,r]
next = l + (steps+1)*k;

diff[next] /= x;
```
Cummulative product by jumping k steps
```cpp
for(int i = 0; i < n; i++){
    if(i-k >= 0)
        diff[i] *= diff[i-k];
}
```
Apply multiplication on nums
```cpp
for(int i = 0; i < n; i++){
    nums[i] *= diff[i];
}
```