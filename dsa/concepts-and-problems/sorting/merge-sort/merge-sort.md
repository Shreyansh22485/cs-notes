# Merge Sort

Merge Sort is a divide-and-conquer algorithm that sorts an array by recursively dividing it into two halves, sorting each half, and then merging the sorted halves back together. It is an efficient, stable, and comparison-based sorting algorithm with a time complexity of O(n log n).

## Key Concepts
- Divide: Split the array into two halves until each subarray contains a single element.
- Conquer: Recursively sort each half.
- Combine: Merge the sorted halves back together.

## C++ Implementation:

```cpp
#include <bits/stdc++.h>
using namespace std;

void merge(vector<int>& arr, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    vector<int> L(n1), R(n2);
    int k = left;
    for (int i = 0; i < n1; i++){
        L[i] = arr[k];
        k++;
    }
    for (int j = 0; j < n2; j++){
        R[j] = arr[k];
        k++;
    }
    int i = 0, j = 0;
    k = left;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

void mergeSort(vector<int>& arr, int left, int right) {
    if (left >= right) return;
    int mid = left + (right - left) / 2;
    mergeSort(arr, left, mid);
    mergeSort(arr, mid + 1, right);
    merge(arr, left, mid, right);
}
```
- Time Complexity: O(n log n) due to the recursive division of the array and merging process.
- Space Complexity: O(n) for the temporary arrays used during the merge process.