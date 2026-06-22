# 74. Search a 2D Matrix

## Problem Statement

You are given an `m x n` integer matrix with the following properties:

- Integers in each row are sorted in ascending order.
- The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return `true` if `target` is in the matrix, otherwise return `false`.

---

## Example 1

```text
Input:
matrix = [[1,3,5,7],
          [10,11,16,20],
          [23,30,34,60]]
target = 3

Output:
true
```

## Example 2

```text
Input:
matrix = [[1,3,5,7],
          [10,11,16,20],
          [23,30,34,60]]
target = 13

Output:
false
```

---

## Approach

Since:

- Every row is sorted.
- The first element of a row is greater than the last element of the previous row.

The entire matrix can be treated as a single sorted array.

### Binary Search

Let:

```text
rows = m
cols = n
```

For an index `mid` in the virtual array:

```cpp
row = mid / cols
col = mid % cols
```

This maps the 1D index back to the 2D matrix position.

Perform standard binary search on the range:

```text
0 → (m * n - 1)
```

---

## C++ Solution

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size();
        int n = matrix[0].size();

        int left = 0;
        int right = m * n - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            int row = mid / n;
            int col = mid % n;

            if (matrix[row][col] == target)
                return true;

            if (matrix[row][col] < target)
                left = mid + 1;
            else
                right = mid - 1;
        }

        return false;
    }
};
```

---

## Dry Run

### Input

```text
matrix =
[
 [1,3,5,7],
 [10,11,16,20],
 [23,30,34,60]
]

target = 16
```

### Virtual Sorted Array

```text
[1,3,5,7,10,11,16,20,23,30,34,60]
```

### Binary Search

```text
mid = 5 → 11
16 > 11

mid = 8 → 23
16 < 23

mid = 6 → 16
Found!
```

Output:

```text
true
```

---

## Complexity Analysis

### Time Complexity

```text
O(log(m × n))
```

### Space Complexity

```text
O(1)
```

---

## Key Concepts

- Binary Search
- Matrix Index Mapping
- Sorted Matrix
- Divide and Conquer

---

## Tags

`Array` `Binary Search` `Matrix`
