# LeetCode 88 - Merge Sorted Array

## Problem Statement

You are given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively.

Merge `nums2` into `nums1` as one sorted array.

The final sorted array should not be returned by the function but instead be stored inside `nums1`.

---

## Example

### Input

```text
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6], n = 3
```

### Output

```text
[1,2,2,3,5,6]
```

### Explanation

The arrays to merge are:

```text
[1,2,3]
[2,5,6]
```

After merging:

```text
[1,2,2,3,5,6]
```

---

## Approach

Since `nums1` contains enough extra space to hold all elements of `nums2`, we can merge the arrays from the **end**.

### Steps

1. Initialize three pointers:
   - `i = m - 1` → last valid element in `nums1`
   - `j = n - 1` → last element in `nums2`
   - `k = m + n - 1` → last position in `nums1`

2. Compare `nums1[i]` and `nums2[j]`.
3. Place the larger element at `nums1[k]`.
4. Move the corresponding pointer backward.
5. If elements remain in `nums2`, copy them into `nums1`.

This avoids overwriting elements in `nums1` and uses no extra space.

---

## C++ Solution

```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i = m - 1;
        int j = n - 1;
        int k = m + n - 1;

        while (i >= 0 && j >= 0) {
            if (nums1[i] > nums2[j]) {
                nums1[k--] = nums1[i--];
            } else {
                nums1[k--] = nums2[j--];
            }
        }

        while (j >= 0) {
            nums1[k--] = nums2[j--];
        }
    }
};
```

---

## Dry Run

### Input

```text
nums1 = [1,2,3,0,0,0]
nums2 = [2,5,6]
```

| i | j | k | Action | nums1 |
|---|---|---|--------|--------|
| 2 | 2 | 5 | Place 6 | [1,2,3,0,0,6] |
| 2 | 1 | 4 | Place 5 | [1,2,3,0,5,6] |
| 2 | 0 | 3 | Place 3 | [1,2,3,3,5,6] |
| 1 | 0 | 2 | Place 2 | [1,2,2,3,5,6] |

Result:

```text
[1,2,2,3,5,6]
```

---

## Complexity Analysis

- **Time Complexity:** `O(m + n)`
- **Space Complexity:** `O(1)`

---

## Key Insight

Merging from the front can overwrite elements in `nums1`. By filling positions from the end, we preserve all values and achieve an in-place merge with constant extra space.
