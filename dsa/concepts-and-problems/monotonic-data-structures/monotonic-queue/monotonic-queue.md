# Monotonic Queue

A queue that always remains in a monotonic order (either increasing or decreasing) is called a monotonic queue.

- Often implemented using a deque (double-ended queue) to allow for efficient insertion and deletion from both ends.

## Monotonic Increasing Queue Template

```cpp
deque<int> dq;

for(int i=0;i<n;i++){
    if(!dq.empty() && dq.front() == i - k){
        dq.pop_front(); // Remove elements that are out of the current window
    }

    while(!dq.empty() && arr[dq.back()] > arr[i]){
        dq.pop_back(); // We want to maintain the increasing order, so we pop elements that are greater than the current element.
    }
    dq.push_back(i); 
    if(i >= k - 1){
        // The front of the deque is the minimum element for the current window
        res.push_back(arr[dq.front()]);
    }
}
```
### How Does this help?
- Monotonic queues are particularly useful for problems where we need to find the minimum in a sliding window of size k.

```cpp
vector<int> slidingWindowMinimum(vector<int>& arr, int k) {
    int n = arr.size();
    vector<int> res;
    deque<int> dq;

    for(int i=0;i<n;i++){
        // Remove elements that are out of the current window
        if(!dq.empty() && dq.front() == i - k){
            dq.pop_front();
        }

        // Maintain the increasing order in the deque
        while(!dq.empty() && arr[dq.back()] > arr[i]){
            dq.pop_back();
        }
        dq.push_back(i);

        // The front of the deque is the minimum element for the current window
        if(i >= k - 1){
            res.push_back(arr[dq.front()]);
        }
    }
    return res;
}
```
- Time Complexity: O(n) where n is the number of elements in the array. Each element is pushed and popped from the deque at most once.
- Space Complexity: O(k) where k is the size of the sliding window, as the deque will contain at most k elements at any time.

# Monotonic Decreasing Queue Template

```cpp
deque<int> dq;
for(int i=0;i<n;i++){
    if(!dq.empty() && dq.front() == i - k){
        dq.pop_front(); // Remove elements that are out of the current window
    }

    while(!dq.empty() && arr[dq.back()] < arr[i]){
        dq.pop_back(); // We want to maintain the decreasing order, so we pop elements that are smaller than the current element.
    }
    dq.push_back(i);
    if(i >= k - 1){
        // The front of the deque is the maximum element for the current window
        res.push_back(arr[dq.front()]);
    }
}
```
### How Does this help?
- Monotonic decreasing queues are particularly useful for problems where we need to find the maximum in a sliding window of size k.

```cpp
vector<int> slidingWindowMaximum(vector<int>& arr, int k) {
    int n = arr.size();
    vector<int> res;
    deque<int> dq;

    for(int i=0;i<n;i++){
        // Remove elements that are out of the current window
        if(!dq.empty() && dq.front() == i - k){
            dq.pop_front();
        }

        // Maintain the decreasing order in the deque
        while(!dq.empty() && arr[dq.back()] < arr[i]){
            dq.pop_back();
        }
        dq.push_back(i);

        // The front of the deque is the maximum element for the current window
        if(i >= k - 1){
            res.push_back(arr[dq.front()]);
        }
    }
    return res;
}
```
- Time Complexity: O(n) where n is the number of elements in the array. Each element is pushed and popped from the deque at most once.
- Space Complexity: O(k) where k is the size of the sliding window, as the deque will contain at most k elements at any time.