# 73. Set Matrix Zeroes

## 🟡 Difficulty
**Medium**

## 🏷️ Topics
- Array
- Matrix

---

## 📖 Problem Statement

Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`.

You must do it **in-place**.

---

## 📝 Example

### Example 1

```text
Input:
matrix = [
  [1,1,1],
  [1,0,1],
  [1,1,1]
]

Output:
[
  [1,0,1],
  [0,0,0],
  [1,0,1]
]
```

### Example 2

```text
Input:
matrix = [
  [0,1,2,0],
  [3,4,5,2],
  [1,3,1,5]
]

Output:
[
  [0,0,0,0],
  [0,4,5,0],
  [0,3,1,0]
]
```

---

## 💡 Approach

Instead of using extra arrays to store rows and columns that need to be zeroed, use the **first row** and **first column** of the matrix as markers.

### Steps

1. Check whether the first row or first column originally contains a zero.
2. Traverse the remaining matrix.
   - If `matrix[i][j] == 0`, mark:
     - `matrix[i][0] = 0`
     - `matrix[0][j] = 0`
3. Traverse the matrix again.
   - If the corresponding row or column marker is `0`, set the cell to `0`.
4. Finally, update the first row and first column if they originally contained a zero.

This achieves the task using **constant extra space**.

---

## ✅ C++ Solution

```cpp
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        int m = matrix.size();
        int n = matrix[0].size();

        bool firstRow = false, firstCol = false;

        for (int i = 0; i < m; i++) {
            if (matrix[i][0] == 0) {
                firstCol = true;
                break;
            }
        }

        for (int j = 0; j < n; j++) {
            if (matrix[0][j] == 0) {
                firstRow = true;
                break;
            }
        }

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }

        if (firstRow) {
            for (int j = 0; j < n; j++)
                matrix[0][j] = 0;
        }

        if (firstCol) {
            for (int i = 0; i < m; i++)
                matrix[i][0] = 0;
        }
    }
};
```

---

## ⏱️ Complexity Analysis

- **Time Complexity:** `O(m × n)`
- **Space Complexity:** `O(1)`

---

## 🎯 Key Insight

- The first row and first column are used as markers to avoid extra memory.
- Separate flags are required because the first row and first column are reused as marker storage.
- This is the optimal in-place solution expected in coding interviews.

---

## 🚀 Tags

`Array` `Matrix` `In-Place` `Simulation`

---

## 📌 Takeaway

Using the first row and first column as marker arrays allows us to solve the problem in **O(m × n)** time and **O(1)** extra space, making it the optimal solution for this problem.
