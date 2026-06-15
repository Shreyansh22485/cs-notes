# Monotonic Stack

A stack that always remains in a monotonic order (either increasing or decreasing) is called a monotonic stack.

## Monotonic Increasing Stack Template

```cpp
Stack<int> st;

for(int i=0;i<n;i++){
    while(!st.empty() && arr[st.top()] > arr[i]){
        st.pop(); // We want to maintain the increasing order, so we pop elements that are greater than the current element.
    }
    st.push(i); 
}
```
### How Does this help?
- This template is useful for problems where we need to find the next or previous smaller element for each element
- The stack will remove elements that are greater than the current element,
because they cannot be the next smaller element for any of the subsequent elements in the array. This ensures that the stack always contains indices of elements in increasing order.
```cpp
vector<int> prevSmallerElement(vector<int>& arr) {
    int n = arr.size();
    vector<int> res(n, -1);
    stack<int> st;

    for(int i=0;i<n;i++){
        while(!st.empty() && arr[st.top()] >= arr[i]){
            st.pop(); // Pop elements that are greater than or equal to the current element
        }
        if(!st.empty()){
            res[i] = st.top(); // The top of the stack is the index of the previous smaller element
        }
        st.push(i); // Push the current index onto the stack
    }
    return res;
}

vector<int> nextSmallerElement(vector<int>& arr) {
    int n = arr.size();
    vector<int> res(n, -1);
    stack<int> st;

    for(int i=n-1;i>=0;i--){
        while(!st.empty() && arr[st.top()] >= arr[i]){
            st.pop(); // Pop elements that are greater than or equal to the current element
        }
        if(!st.empty()){
            res[i] = st.top(); // The top of the stack is the index of the next smaller element
        }
        st.push(i); // Push the current index onto the stack
    }
    return res;
}

vector<int> prevSmallerOrEqualElement(vector<int>& arr) {
    int n = arr.size();
    vector<int> res(n, -1);
    stack<int> st;

    for(int i=0;i<n;i++){
        while(!st.empty() && arr[st.top()] > arr[i]){
            st.pop(); // Pop elements that are greater than the current element
        }
        if(!st.empty()){
            res[i] = st.top(); // The top of the stack is the index of the previous smaller or equal element
        }
        st.push(i); // Push the current index onto the stack
    }
    return res;
}

vector<int> nextSmallerOrEqualElement(vector<int>& arr) {
    int n = arr.size();
    vector<int> res(n, -1);
    stack<int> st;

    for(int i=n-1;i>=0;i--){
        while(!st.empty() && arr[st.top()] > arr[i]){
            st.pop(); // Pop elements that are greater than the current element
        }
        if(!st.empty()){
            res[i] = st.top(); // The top of the stack is the index of the next smaller or equal element
        }
        st.push(i); // Push the current index onto the stack
    }
    return res;
}

```
- Time Complexity: O(N) where N is the number of elements in the array. Each element is pushed and popped at most once.
- Space Complexity: O(N) in the worst case when the stack contains all elements of the array.

## Monotonic Decreasing Stack Template

```cpp
Stack<int> st;
for(int i=0;i<n;i++){
    while(!st.empty() && arr[st.top()] < arr[i]){
        st.pop(); // We want to maintain the decreasing order, so we pop elements that are smaller than the current element.
    }
    st.push(i); 
}
```
### How Does this help?
- This template is useful for problems where we need to find the next or previous greater element for each element
- The stack will remove elements that are smaller than the current element, because they cannot be the next greater element for any of the subsequent elements in the array. This ensures that the stack always contains indices of elements in decreasing order.
```cpp
vector<int> prevGreaterElement(vector<int>& arr) {
    int n = arr.size();
    vector<int> res(n, -1);
    stack<int> st;

    for(int i=0;i<n;i++){
        while(!st.empty() && arr[st.top()] <= arr[i]){
            st.pop(); // Pop elements that are smaller than or equal to the current element
        }
        if(!st.empty()){
            res[i] = st.top(); // The top of the stack is the index of the previous greater element
        }
        st.push(i); // Push the current index onto the stack
    }
    return res;
}

vector<int> nextGreaterElement(vector<int>& arr) {
    int n = arr.size();
    vector<int> res(n, -1);
    stack<int> st;

    for(int i=n-1;i>=0;i--){
        while(!st.empty() && arr[st.top()] <= arr[i]){
            st.pop(); // Pop elements that are smaller than or equal to the current element
        }
        if(!st.empty()){
            res[i] = st.top(); // The top of the stack is the index of the next greater element
        }
        st.push(i); // Push the current index onto the stack
    }
    return res;
}

vector<int> prevGreaterOrEqualElement(vector<int>& arr) {
    int n = arr.size();
    vector<int> res(n, -1);
    stack<int> st;

    for(int i=0;i<n;i++){
        while(!st.empty() && arr[st.top()] < arr[i]){
            st.pop(); // Pop elements that are smaller than the current element
        }
        if(!st.empty()){
            res[i] = st.top(); // The top of the stack is the index of the previous greater or equal element
        }
        st.push(i); // Push the current index onto the stack
    }
    return res;
}

vector<int> nextGreaterOrEqualElement(vector<int>& arr) {
    int n = arr.size();
    vector<int> res(n, -1);
    stack<int> st;

    for(int i=n-1;i>=0;i--){
        while(!st.empty() && arr[st.top()] < arr[i]){
            st.pop(); // Pop elements that are smaller than the current element
        }
        if(!st.empty()){
            res[i] = st.top(); // The top of the stack is the index of the next greater or equal element
        }
        st.push(i); // Push the current index onto the stack
    }
    return res;
}
```
- Time Complexity: O(N) where N is the number of elements in the array. Each element is pushed and popped at most once.
- Space Complexity: O(N) in the worst case when the stack contains all elements of the array.
