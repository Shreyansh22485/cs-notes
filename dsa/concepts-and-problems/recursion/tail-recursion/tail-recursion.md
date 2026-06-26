# Tail Recursion

Form of recursion where the recursive call is the last operation in the function. In tail recursion, there is no need to keep track of previous states, which allows for optimizations by the compiler or interpreter. This can lead to improved performance and reduced stack usage.

```cpp
int solve(){
    // Base case
    if (/* condition */) {
        return /* base case value */;
    }
    

    return solve();
}
```

## Example of Tail Recursion vs Non-Tail Recursion

Non Tail Recursion:

```cpp
int factorial(int n) {
    if (n <= 1) {
        return n;
    }
    return n * factorial(n - 1);
}
```


Tail Recursion:
```cpp
int factorial_tail(int n, int prod) {
    if (n <= 1) {
        return prod;
    }
    return factorial_tail(n - 1, n * prod);
}
```

**In case of Tail Recursion, the system stack does not need to keep track of previous states, which can lead to optimizations because of space efficiency.**

### Examples
- Preorder Traversal of a Binary Tree
- Inorder Traversal of a Binary Tree

*Note: Postorder traversal is not tail recursive.*
