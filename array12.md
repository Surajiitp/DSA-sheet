# 31. Next Permutation

## Problem Statement

A permutation of an array of integers is an arrangement of its members into a sequence or linear order.

Given an array of integers `nums`, find the next permutation of `nums`.

The replacement must be **in-place** and use only constant extra memory.

---

## Example 1

```text
Input: nums = [1,2,3]
Output: [1,3,2]
```

## Example 2

```text
Input: nums = [3,2,1]
Output: [1,2,3]
```

## Example 3

```text
Input: nums = [1,1,5]
Output: [1,5,1]
```

---

## Approach

To find the next lexicographically greater permutation:

### Step 1: Find the Pivot
Traverse from right to left and find the first index `i` such that:

```cpp
nums[i] < nums[i + 1]
```

This element is called the **pivot**.

### Step 2: Find the Next Greater Element
Again traverse from the right and find the first element greater than `nums[i]`.

### Step 3: Swap
Swap the pivot with that element.

### Step 4: Reverse the Remaining Part
Reverse the subarray from `i + 1` to the end.

If no pivot exists, the array is in descending order, so simply reverse the entire array.

---

## Dry Run

### Input

```text
[1,2,3]
```

### Find Pivot

```text
2 < 3
Pivot = 2
```

### Find Next Greater Element

```text
3 > 2
```

### Swap

```text
[1,3,2]
```

### Reverse Suffix

```text
[1,3,2]
```

### Output

```text
[1,3,2]
```

---

## C++ Solution

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int n = nums.size();

        int i = n - 2;

        while (i >= 0 && nums[i] >= nums[i + 1]) {
            i--;
        }

        if (i >= 0) {
            int j = n - 1;

            while (nums[j] <= nums[i]) {
                j--;
            }

            swap(nums[i], nums[j]);
        }

        reverse(nums.begin() + i + 1, nums.end());
    }
};
```

---

## Complexity Analysis

| Complexity | Value |
|------------|--------|
| Time | O(n) |
| Space | O(1) |

---

## Key Concepts

- Array
- Two Pointers
- Greedy
- Permutations

---

## LeetCode Link

https://leetcode.com/problems/next-permutation/
