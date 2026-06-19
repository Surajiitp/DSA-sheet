# 75. Sort Colors

## Problem Statement

Given an array `nums` with `n` objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent.

We use the integers:

- `0` → Red
- `1` → White
- `2` → Blue

You must solve this problem without using the library's sort function.

### Example 1

```text
Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

### Example 2

```text
Input: nums = [2,0,1]
Output: [0,1,2]
```

---

## Approach: Dutch National Flag Algorithm

We maintain three pointers:

- `low` → position where next `0` should be placed
- `mid` → current element being processed
- `high` → position where next `2` should be placed

### Rules

1. If `nums[mid] == 0`
   - Swap `nums[low]` and `nums[mid]`
   - Increment `low` and `mid`

2. If `nums[mid] == 1`
   - Increment `mid`

3. If `nums[mid] == 2`
   - Swap `nums[mid]` and `nums[high]`
   - Decrement `high`

This partitions the array into:

```text
[0 ... low-1]      -> all 0s
[low ... mid-1]    -> all 1s
[mid ... high]     -> unknown
[high+1 ... n-1]   -> all 2s
```

---

## C++ Solution

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int low = 0;
        int mid = 0;
        int high = nums.size() - 1;

        while (mid <= high) {
            if (nums[mid] == 0) {
                swap(nums[low], nums[mid]);
                low++;
                mid++;
            }
            else if (nums[mid] == 1) {
                mid++;
            }
            else {
                swap(nums[mid], nums[high]);
                high--;
            }
        }
    }
};
```

---

## Dry Run

```text
nums = [2,0,2,1,1,0]

low = 0, mid = 0, high = 5

2 → swap(mid, high)
[0,0,2,1,1,2]

0 → swap(low, mid)
[0,0,2,1,1,2]
low=1, mid=1

0 → swap(low, mid)
[0,0,2,1,1,2]
low=2, mid=2

2 → swap(mid, high)
[0,0,1,1,2,2]
high=4

1 → mid++
1 → mid++

Finished
```

---

## Complexity Analysis

### Time Complexity

```text
O(n)
```

Each element is processed at most once.

### Space Complexity

```text
O(1)
```

Only three pointers are used.

---

## Key Concepts

- Two Pointers
- Three Pointers
- Dutch National Flag Algorithm
- In-Place Sorting
- Array Partitioning

---

## LeetCode Link

https://leetcode.com/problems/sort-colors/
